---
title: Compilazione, distribuzione e debug di oggetti personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 22b7d07752c6a9df5f0b100c0d16b78a86125f04
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362853"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>Compilazione, distribuzione e debug di oggetti personalizzati
  Dopo avere scritto il codice per un oggetto personalizzato per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario compilare l'assembly, distribuirlo, integrarlo in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] per renderlo disponibile per l'utilizzo nei pacchetti, quindi sottoporlo a test e debug.  
  
##  <a name="top"></a>Passaggi per la compilazione, la distribuzione e il debug di un oggetto personalizzato per Integration Services  
 La funzionalità personalizzata per l'oggetto è già stata scritta. A questo punto, è necessario testarla e renderla disponibile per gli utenti. I passaggi sono molto simili per tutti i tipi di oggetti personalizzati che è possibile creare per [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Di seguito sono riportati i passaggi da completare per la compilazione, la distribuzione e il debug:  
  
1.  [Firmare](#signing) l'assembly da generare con un nome sicuro.  
  
2.  [Compilare](#building) l'assembly.  
  
3.  [Distribuire](#deploying) l'assembly spostandolo o copiandolo nella cartella di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] appropriata.  
  
4.  [Installare](#installing) l'assembly nella Global Assembly Cache.  
  
     L'oggetto viene automaticamente aggiunto alla Casella degli strumenti.  
  
5.  Se necessario, [risolvere i problemi](#troubleshooting) della distribuzione.  
  
6.  [Eseguire il test](#testing) e il debug del codice.  
  
##  <a name="signing"></a> Firma dell'assembly  
 Quando un assembly deve essere condiviso, è necessario installarlo nella Global Assembly Cache. Una volta aggiunto alla Global Assembly Cache, l'assembly può essere utilizzato da applicazioni come [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Un requisito della Global Assembly Cache è che l'assembly deve essere firmato con un nome sicuro che garantisca che sia globalmente univoco. Un assembly con nome sicuro dispone di un nome completo che include il nome, la lingua, la chiave pubblica e il numero di versione dell'assembly. Tali informazioni vengono utilizzate dal runtime per individuare l'assembly e distinguerlo da altri assembly aventi lo stesso nome.  
  
 Per firmare un assembly con un nome sicuro, è innanzitutto necessario avere o creare una coppia di chiavi pubblica/privata. Questa coppia di chiavi di crittografia, pubblica e privata, viene utilizzata durante la compilazione per creare un assembly con nome sicuro.  
  
 Per ulteriori informazioni sui nomi sicuri e sui passaggi che è necessario eseguire per firmare un assembly, vedere gli argomenti seguenti nella documentazione relativa a [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK:  
  
-   Assembly con nomi sicuri  
  
-   Creazione di una coppia di chiavi  
  
-   Firma di un assembly con un nome sicuro  
  
 È possibile firmare facilmente l'assembly con un nome sicuro in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] durante la compilazione. Nella finestra di dialogo **Proprietà progetto** selezionare la scheda **Firma**. Selezionare l'opzione **Firma assembly** e quindi specificare il percorso del file di chiave (con estensione snk).  
  
##  <a name="building"></a> Compilazione dell'assembly  
 Dopo aver firmato il progetto, è necessario compilare o ricompilare il progetto o la soluzione tramite i comandi disponibili nel menu **Compila** di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La soluzione può contenere un progetto distinto per un'interfaccia utente personalizzata, che deve essere firmato con un nome sicuro e può essere compilato contemporaneamente.  
  
 Il metodo più semplice per eseguire i due passaggi successivi, ovvero la distribuzione dell'assembly e l'installazione nella Global Assembly Cache, consiste nel generare script per questi passaggi come evento di post-compilazione in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Gli eventi di compilazione sono disponibili dalla pagina **Compilazione** di Proprietà progetto per un progetto [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e dalla pagina **Eventi di compilazione** per un progetto C#. Per utilità del prompt dei comandi come **gacutil.exe** è necessario specificare il percorso completo. È necessario racchiudere tra virgolette i percorsi che contengono spazi e le macro, ad esempio $(TargetPath), che si espandono in percorsi che contengono spazi.  
  
 Di seguito è riportato un esempio di una riga di comando per eventi di post-compilazione per un provider di log personalizzato:  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\120\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a> Distribuzione dell'assembly  
 Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] individua gli oggetti personalizzati disponibili per l'uso nei pacchetti enumerando i file trovati in una serie di cartelle create durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Quando il valore predefinito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono usate le impostazioni di installazione, questo set di cartelle si trova sotto **C:\Program Files\Microsoft SQL Server\120\DTS**. Tuttavia se si crea un programma di installazione per l'oggetto personalizzato, è consigliabile controllare il valore della **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\Setup\DtsPath** chiave del Registro di sistema per verificare il percorso di questo oggetto cartella.  
  
 È possibile inserire l'assembly nella cartella in due modi:  
  
-   Spostare o copiare l'assembly compilato nella cartella appropriata dopo averlo compilato. Per praticità, è possibile includere il comando di copia in un evento di post-compilazione.  
  
-   Compilare l'assembly direttamente nella cartella appropriata.  
  
 Le cartelle di distribuzione seguenti sotto **C:\Program Files\Microsoft SQL Server\120\DTS** vengono usati per i vari tipi di oggetti personalizzati:  
  
|Oggetto personalizzato|Cartella di distribuzione|  
|-------------------|-----------------------|  
|Attività|Attività|  
|Gestione connessione|Connessioni|  
|Provider di log|LogProviders|  
|Componente del flusso di dati|PipelineComponents|  
  
> [!NOTE]  
>  Gli assembly vengono copiati in queste cartelle per supportare l'enumerazione degli oggetti personalizzati disponibili, quali attività, gestioni connessioni e così via. Pertanto, non è necessario distribuire in queste cartelle gli assembly che contengono solo l'interfaccia utente personalizzata per gli oggetti personalizzati.  
  
##  <a name="installing"></a>Installazione dell'assembly nella Global Assembly Cache  
 Per installare l'assembly attività nella Global Assembly Cache, usare lo strumento da riga di comando **gacutil.exe** oppure trascinare gli assembly nella directory `%system%\assembly`. Per praticità, è anche possibile includere la chiamata a **gacutil.exe** in un evento di post-compilazione.  
  
 Il comando seguente installa un componente denominato *MyTask.dll* nella Global Assembly Cache tramite **gacutil.exe**.  
  
 `gacutil /iF MyTask.dll`  
  
 Dopo l'installazione di una nuova versione dell'oggetto personalizzato, è necessario chiudere e riaprire Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Se sono state installate versioni precedenti dell'oggetto personalizzato nella Global Assembly Cache, è necessario rimuoverle prima di installare la nuova versione. Per disinstallare un assembly, eseguire **gacutil.exe** e specificare il nome dell'assembly con l'opzione `/u`.  
  
 Per ulteriori informazioni sulla Global Assembly Cache, vedere lo strumento corrispondente (Gactutil.exe) in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Tools.  
  
##  <a name="troubleshooting"></a> Risoluzione dei problemi della distribuzione  
 Se l'oggetto personalizzato è visualizzato nella **casella degli strumenti** o nell'elenco di oggetti disponibili ma non è possibile aggiungerlo a un pacchetto, provare a effettuare le operazioni seguenti:  
  
1.  Verificare se nella Global Assembly Cache sono disponibili più versioni del componente. In caso affermativo, è possibile che la finestra di progettazione non sia in grado di caricare il componente. Eliminare tutte le istanze dell'assembly dalla Global Assembly Cache, quindi aggiungere nuovamente l'assembly.  
  
2.  Verificare che nella cartella di distribuzione esista una singola istanza dell'assembly.  
  
3.  Aggiornare la casella degli strumenti.  
  
4.  Connettere [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] a **devenv.exe** e impostare un punto di interruzione per eseguire le istruzioni del codice di inizializzazione e assicurarsi che non si verifichino eccezioni.  
  
##  <a name="testing"></a> Test e debug del codice  
 L'approccio più semplice per l'esecuzione del debug dei metodi di runtime di un oggetto personalizzato consiste nell'avviare **dtexec.exe** da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] dopo aver compilato l'oggetto e nell'eseguire quindi un pacchetto che usa il componente.  
  
 Se si desidera eseguire il debug di metodi della fase di progettazione del componente, ad esempio il `Validate` metodo, aprire un pacchetto che utilizza il componente in una seconda istanza di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e collegare alla relativa **devenv.exe** processo.  
  
 Se si vuole eseguire il debug anche dei metodi di runtime del componente quando un pacchetto è aperto e in esecuzione in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)], è necessario forzare una pausa nell'esecuzione del pacchetto in modo che sia possibile connettersi anche al processo **DtsDebugHost.exe**.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>Per eseguire il debug dei metodi di runtime di un oggetto tramite connessione a dtexec.exe  
  
1.  Firmare e compilare il progetto nella configurazione di debug, distribuirlo e installarlo nella Global Assembly Cache come descritto in questo argomento.  
  
2.  Nel **Debug** scheda della finestra **le proprietà del progetto**, selezionare **Avvia programma esterno** come il **azione di avvio**e individuare  **DTExec.exe**, cui è installato per impostazione predefinita in C:\Program Files\Microsoft SQL Server\120\DTS\Binn.  
  
3.  Nella casella di testo **Opzioni della riga di comando** in **Opzioni di avvio** immettere gli argomenti della riga di comando richiesti per eseguire un pacchetto in cui viene usato il componente. In genere l'argomento della riga di comando sarà costituito dall'opzione /F[ILE] seguita dal percorso e dal nome del file con estensione dtsx. Per altre informazioni, vedere [dtexec Utility](../packages/dtexec-utility.md).  
  
4.  Impostare i punti di interruzione nel codice sorgente, laddove appropriato, nei metodi di runtime del componente.  
  
5.  Eseguire il progetto.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>Per eseguire il debug dei metodi della fase di progettazione di un oggetto personalizzato tramite connessione a SQL Server Data Tools  
  
1.  Firmare e compilare il progetto nella configurazione di debug, distribuirlo e installarlo nella Global Assembly Cache come descritto in questo argomento.  
  
2.  Impostare i punti di interruzione nel codice sorgente, laddove appropriato, nei metodi della fase di progettazione dell'oggetto personalizzato.  
  
3.  Aprire una seconda istanza di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e caricare un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente un pacchetto in cui è utilizzato l'oggetto personalizzato.  
  
4.  Dalla prima istanza di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], connettersi alla seconda istanza di **devenv.exe** in cui è caricato il pacchetto scegliendo **Connetti a processo** dal menu **Debug** della prima istanza.  
  
5.  Eseguire il pacchetto dalla seconda istanza di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>Per eseguire il debug dei metodi di runtime di un oggetto personalizzato tramite connessione a SQL Server Data Tools  
  
1.  Dopo avere completato i passaggi descritti nella procedura precedente, forzare una pausa nell'esecuzione del pacchetto in modo che sia possibile connettersi a **DtsDebugHost.exe**. Per forzare questa pausa, è possibile aggiungere un punto di interruzione all'evento `OnPreExecute` oppure aggiungere un'attività Script al progetto e passare allo script che visualizza una finestra di messaggio modale.  
  
2.  Eseguire il pacchetto. Quando si verifica la pausa, passare all'istanza di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] in cui è aperto il progetto di codice e scegliere **Connetti a processo** dal menu **Debug**. Assicurarsi di connettersi all'istanza di **DtsDebugHost.exe** riportata come **Gestito, x86** nella colonna **Tipo** e non all'istanza indicata solo come **x86**.  
  
3.  Tornare al pacchetto in pausa e continuare oltre il punto di interruzione oppure fare clic su **OK** per annullare la finestra di messaggio generata dall'attività Script, quindi continuare con l'esecuzione e il debug del pacchetto.  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di oggetti personalizzati per Integration Services](developing-custom-objects-for-integration-services.md)   
 [Persistenza degli oggetti personalizzati](persisting-custom-objects.md)   
 [Strumenti per la risoluzione dei problemi relativi allo sviluppo dei pacchetti](../troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
