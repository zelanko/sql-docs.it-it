---
title: Utilità dtexec | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 53ddc509c4f44677a2504b791502d530c2104bf5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964871"
---
# <a name="dtexec-utility"></a>Utilità dtexec
  L' `dtexec` utilità del prompt dei comandi viene utilizzata per configurare ed eseguire i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti. Con l'utilità `dtexec` è possibile accedere a tutte le funzionalità di configurazione ed esecuzione dei pacchetti quali parametri, connessioni, proprietà, variabili, registrazione e indicatori di stato. L' `dtexec` utilità consente di caricare i pacchetti da queste origini: il [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server, un file di progetto con estensione ispac, un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, l' [!INCLUDE[ssIS](../../includes/ssis-md.md)] Archivio pacchetti e il file System.  
  
> [!NOTE]  
>  Quando si utilizza la versione dell'utilità `dtexec` fornita con [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] per eseguire un pacchetto di [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] il pacchetto viene temporaneamente aggiornato a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]. Tuttavia, non è possibile utilizzare l'utilità `dtexec` per salvare queste modifiche aggiornate. Per ulteriori informazioni su come aggiornare in modo permanente un pacchetto a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] , vedere [upgrade Integration Services packages](../install-windows/upgrade-integration-services-packages.md).  
  
 Questo argomento include le sezioni seguenti:  
  
-   [Server Integration Services e file di progetto](#server)  
  
-   [Considerazioni sull'installazione in computer a 64 bit](#bit)  
  
-   [Considerazioni sui computer con installazioni side-by-side](#side)  
  
-   [Fasi di esecuzione](#phases)  
  
-   [Codici di uscita restituiti](#exit)  
  
-   [Regole della sintassi](#syntaxRules)  
  
-   [Utilizzo di dtexec da xp_cmdshell](#cmdshell)  
  
-   [Sintassi](#syntax)  
  
-   [Parametri](#parameter)  
  
-   [Osservazioni:](#remark)  
  
-   [esempi](#example)  
  
##  <a name="integration-services-server-and-project-file"></a><a name="server"></a>Server Integration Services e file di progetto  
 Quando si utilizza `dtexec` per eseguire i pacchetti sul [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server, `dtexec` chiama il [catalogo. create_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog. set_execution_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) e [Catalog. start_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) stored procedure per creare un'esecuzione, impostare i valori dei parametri e avviare l'esecuzione. Tutti i log di esecuzione possono essere visualizzati dal server nelle viste correlate o tramite report standard disponibili in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sui report, vedere [Report per il server Integration Services](../reports-for-the-integration-services-server.md).  
  
 Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Quando si utilizza `dtexec` per eseguire un pacchetto dal file di progetto con estensione ispac, le opzioni correlate sono /Proj[ect] e /Pack[age] utilizzate per specificare il percorso del progetto e il nome di flusso del pacchetto. Quando si converte un progetto nel modello di distribuzione del progetto eseguendo la **Conversione guidata progetto di Integration Services** da [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], tramite la procedura guidata viene generato un file di progetto con estensione ispac. Per altre informazioni, vedere [Distribuire progetti nel server Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 È possibile utilizzare `dtexec` con gli strumenti di pianificazione di terze parti per pianificare i pacchetti distribuiti nel [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server.  
  
##  <a name="installation-considerations-on-64-bit-computers"></a><a name="bit"></a> Considerazioni sull'installazione in computer a 64 bit  
 In un computer a 64 bit con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene installata una versione a 64 bit dell'utilità `dtexec` (dtexec.exe). Se è necessario eseguire alcuni pacchetti nella modalità 32 bit, è necessario installare la versione a 32 bit dell'utilità `dtexec`. Per installare la versione a 32 bit dell'utilità `dtexec`, è necessario selezionare gli strumenti client o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] durante l'installazione.  
  
 Per impostazione predefinita, un computer a 64 bit contenente le versioni a 64 bit e a 32 bit di un'utilità del prompt dei comandi di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installata eseguirà la versione a 32 bit al prompt dei comandi. Viene eseguita la versione a 32 bit perché il percorso della directory della versione a 32 bit compare nella variabile di ambiente PATH prima del percorso della directory della versione a 64 bit. In genere, il percorso della directory a 32 bit è *\<drive>* : \Program Files (x86) \Microsoft SQL Server\110\DTS\Binn, mentre il percorso della directory a 64 bit è *\<drive>* : \Programmi\microsoft SQL Server\110\DTS\Binn.  
  
> [!NOTE]  
>  Se si utilizza SQL Server Agent per eseguire l'utilità, verrà automaticamente utilizzata la versione a 64 bit dell'utilità. Per trovare l'eseguibile corretto per l'utilità, SQL Server Agent utilizza il Registro di sistema, non la variabile di ambiente PATH.  
  
 Per assicurarsi di eseguire la versione a 64 bit dell'utilità al prompt dei comandi, è possibile eseguire una delle azioni seguenti:  
  
-   Aprire una finestra del prompt dei comandi, passare alla directory che contiene la versione a 64 bit dell'utilità ( *\<drive>* : \Programmi\Microsoft SQL Server\110\DTS\Binn), quindi eseguire l'utilità da quel percorso.  
  
-   Al prompt dei comandi, eseguire l'utilità immettendo il percorso completo ( *\<drive>* : \Programmi\Microsoft SQL Server\110\DTS\Binn) della versione a 64 bit dell'utilità.  
  
-   Modificare in modo definitivo l'ordine dei percorsi nella variabile di ambiente PATH inserendo il percorso 64 bit ( *\<drive>* : \Programmi\Microsoft SQL Server\110\DTS\Binn) prima del percorso di 32 bit ( *\<drive>* : \ Programmi (x86) \Microsoft SQL Server\110\DTS\Binn) nella variabile.  
  
##  <a name="considerations-on-computers-with-side-by-side-installations"></a><a name="side"></a> Considerazioni sui computer con installazioni side-by-side  
 Se [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] è installato in un computer con [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], vengono installate più versioni dell'utilità `dtexec`.  
  
 Per assicurarsi di eseguire la versione corretta dell'utilità, al prompt dei comandi eseguire l'utilità immettendo il percorso completo ( *\<drive>* : \programmi\microsoft SQL Server \\<versione \> \DTS\Binn).  
  
##  <a name="phases-of-execution"></a><a name="phases"></a>Fasi di esecuzione  
 L'esecuzione di questa utilità si articola nelle quattro fasi descritte di seguito.  
  
1.  Determinazione dell'origine del comando: il prompt dei comandi legge l'elenco delle opzioni e degli argomenti specificati. Tutte le fasi successive vengono ignorate se viene rilevata un'opzione **/?** o **/HELP** .  
  
2.  Fase di caricamento del pacchetto: viene caricato il pacchetto specificato dall' `/SQL` opzione, **/file**o `/DTS` .  
  
3.  Configurazione: le opzioni vengono elaborate nell'ordine riportato di seguito.  
  
    -   Opzioni che impostano i flag, le variabili e le proprietà dei pacchetti.  
  
    -   Opzioni che verificano la versione e la build del pacchetto.  
  
    -   Opzioni che configurano il comportamento dell'utilità in fase di esecuzione, ad esempio la creazione di report.  
  
4.  Convalida ed esecuzione: il pacchetto viene eseguito oppure convalidato ma non eseguito se è stata specificata l'opzione **/VALIDATE** .  
  
##  <a name="exit-codes-returned"></a><a name="exit"></a>Codici di uscita restituiti  
 **Codici di uscita restituiti dall'utilità dtexec**  
  
 Durante l'esecuzione di un pacchetto è possibile che `dtexec` restituisca un codice di uscita. Il codice di uscita viene utilizzato per popolare la variabile ERRORLEVEL, il cui valore può essere testato nelle istruzioni condizionali o nella logica di diramazione in un file batch. Nella tabella seguente vengono elencati i valori che l'utilità `dtexec` può impostare all'uscita.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|Il pacchetto è stato eseguito correttamente.|  
|1|Il pacchetto non è stato eseguito.|  
|3|L'esecuzione del pacchetto è stata annullata dall'utente.|  
|4|L'utilità non è stata in grado di individuare il pacchetto richiesto. Risulta impossibile trovare il pacchetto.|  
|5|L'utilità non è stata in grado di caricare il pacchetto richiesto. Risulta impossibile caricare il pacchetto.|  
|6|L'utilità ha rilevato un errore interno oppure un errore sintattico o semantico nella riga di comando.|  
  
##  <a name="syntax-rules"></a><a name="syntaxRules"></a>Regole di sintassi  
 **Regole di sintassi dell'utilità**  
  
 Tutte le opzioni devono essere precedute da una barra (/) o un segno meno (-). Le opzioni riportate di seguito sono precedute da una barra (/), che può tuttavia essere sostituita dal segno meno (-).  
  
 Se l'argomento contiene uno spazio, deve essere racchiuso tra virgolette. Se non è racchiuso tra virgolette, un argomento non può contenere spazi vuoti.  
  
 Le virgolette doppie all'interno di stringhe racchiuse tra virgolette rappresentano virgolette singole di escape.  
  
 Le opzioni e gli argomenti, escluse le password, non fanno distinzione tra maiuscole e minuscole.  
  
##  <a name="using-dtexec-from-the-xp_cmdshell"></a><a name="cmdshell"></a>Uso di dtexec dalla xp_cmdshell  
 **Utilizzo di dtexec da xp_cmdshell**  
  
 È possibile eseguire dtexec dal prompt di **xp_cmdshell** . Nell'esempio seguente viene illustrato come eseguire un pacchetto denominato UpsertData.dtsx e ignorare il codice restituito:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 Nell'esempio seguente viene illustrato come eseguire lo stesso pacchetto e acquisire il codice restituito:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> [!IMPORTANT]  
>  Nelle nuove installazioni, in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l'opzione **xp_cmdshell** risulta disabilitata per impostazione predefinita. L'opzione può essere abilitata eseguendo la stored procedure di sistema **sp_configure** . Per altre informazioni, vedere [Opzione di configurazione del server xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
##  <a name="syntax"></a><a name="syntax"></a>Sintassi  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameters"></a><a name="parameter"></a> Parametri  
  
-   **/?** [*option_name*]: facoltativo. Consente di visualizzare le opzioni del prompt dei comandi o le informazioni della Guida relative all'opzione *option_name* specificata e quindi di chiudere l'utilità.  
  
     Se si specifica un argomento di *option_name* , `dtexec` viene avviata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la documentazione online di e viene visualizzato l'argomento relativo all'utilità dtexec.  
  
-   **/Nome CA [llerInfo]**:   
                  Facoltativa. Specifica informazioni aggiuntive per l'esecuzione di un pacchetto. Quando si esegue un pacchetto utilizzando SQL Server Agent, tramite l'agente è possibile impostare questo argomento per specificare che l'esecuzione del pacchetto venga richiamata da SQL Server Agent. Questo parametro viene ignorato quando l'utilità `dtexec` viene eseguita dalla riga di comando.  
  
-   **/CheckF[ile]** _filespec_:   
                  Facoltativa. Imposta la `CheckpointFileName` proprietà del pacchetto sul percorso e sul file specificati in *filespec*. Questo file viene utilizzato quando il pacchetto viene riavviato. Se si specifica questa opzione ma si omette il valore del nome file, la proprietà `CheckpointFileName` del pacchetto viene impostata su una stringa vuota. Se si omette questa opzione, i valori nel pacchetto vengono conservati.  
  
-   **/CheckP [ointing]** _{ON\OFF}_:   
                  Facoltativa. Consente di impostare un valore che determina se il pacchetto utilizzerà i checkpoint durante l'esecuzione. Il valore **on** indica che un pacchetto la cui esecuzione ha avuto esito negativo deve essere rieseguito. In questo caso, il motore di run-time utilizza il file del checkpoint per riavviare il pacchetto dal punto in cui si è verificato l'errore.  
  
     Il valore predefinito è on se l'opzione viene dichiarata senza un valore. L'esecuzione del pacchetto avrà esito negativo se il valore viene impostato su on, ma non risulta possibile trovare il file del checkpoint. Se si omette questa opzione, il valore impostato nel pacchetto viene conservato. Per ulteriori informazioni, vedere [Restart Packages by Using Checkpoints](restart-packages-by-using-checkpoints.md).  
  
     L'opzione **/CheckPointing on on** di dtexec equivale a impostare la `SaveCheckpoints` proprietà del pacchetto su true e la `CheckpointUsage` proprietà su Always.  
  
-   **/Com[mandFile]** _filespec_:   
                  (Facoltativo). Specifica le opzioni di comando eseguite con `dtexec`. Il file specificato in *filespec* viene aperto e le relative opzioni vengono lette finché non viene rilevata la fine del file. *filespec* è un file di testo. L'argomento *filespec* consente di specificare il nome e il percorso del file di comando da associare all'esecuzione del pacchetto.  
  
-   **/Conf [igFile]** _filespec_: facoltativo. Consente di specificare un file di configurazione da cui estrarre valori. Se si utilizza questa opzione, è possibile impostare una configurazione della fase di esecuzione diversa rispetto alla configurazione specificata in fase di progettazione per il pacchetto. È possibile archiviare impostazioni di configurazione diverse in un file di configurazione XML e quindi caricare tali impostazioni tramite l'opzione **/ConfigFile** prima dell'esecuzione del pacchetto.  
  
     È possibile usare l'opzione **/ConfigFile** per caricare in fase di esecuzione configurazioni aggiuntive non specificate in fase di progettazione. Non è tuttavia possibile usare l'opzione **/ConfigFile** per sostituire valori configurati specificati anche in fase di progettazione. Per informazioni sull'applicazione delle configurazioni dei pacchetti, vedere [Package Configurations](../package-configurations.md).  
  
-   **/Conn[ection]** _id_or_name;connection_string [[;id_or_name;connection_string]...]_:   
                  Facoltativa. Consente di specificare che la gestione connessione con il nome o il GUID indicato si trova nel pacchetto e che è stata specificata una stringa di connessione.  
  
     Questa opzione richiede che vengano specificati entrambi i parametri: il nome o il GUID della gestione connessione deve essere specificato nell'argomento *id_or_name* , mentre nell'argomento *connection_string* deve essere specificata una stringa di connessione valida. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../connection-manager/integration-services-ssis-connections.md).  
  
     In fase di esecuzione è possibile usare l'opzione **/Connection** per caricare le configurazioni di pacchetto da una posizione diversa da quella specificata in fase di progettazione. I valori di queste configurazioni sostituiscono i valori specificati in origine. È tuttavia possibile usare l'opzione **/Connection** solo per le configurazioni che usano una gestione connessione, ad esempio le configurazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per comprendere il modo in cui vengono applicate le configurazioni dei pacchetti, vedere [configurazioni di pacchetto](../package-configurations.md) e [modifiche del comportamento per le funzionalità Integration Services di SQL Server 2014](../behavior-changes-to-integration-services-features-in-sql-server-2014.md).  
  
-   **Opzioni/Cons [oleLog]** [[*DisplayOptions*]; [ *list_options*; *src_name_or_guid*] ...]: Facoltativo. Consente di visualizzare le voci di log specificate nella console durante l'esecuzione del pacchetto. Se questa opzione viene omessa, non verrà visualizzata alcuna voce di log nella console. Se si specifica l'opzione senza tuttavia alcun parametro per limitare la visualizzazione, verrà visualizzata ogni voce di log. Per limitare il numero di voci visualizzate nella console, è possibile specificare le colonne da visualizzare tramite il parametro *displayoptions* e limitare i tipi di voci di log tramite il parametro *list_options* .  
  
    > [!NOTE]  
    >  Quando si esegue un pacchetto nel [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server utilizzando il `/ISSERVER` parametro, l'output della console è limitato e la maggior parte delle opzioni **Opzioni/Cons [oleLog]** non è applicabile. Tutti i log di esecuzione possono essere visualizzati dal server nelle viste correlate o tramite report standard disponibili in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sui report, vedere [Report per il server Integration Services](../reports-for-the-integration-services-server.md).  
  
     Sono disponibili i valori *displayoptions* seguenti:  
  
    -   N (Name)  
  
    -   C (Computer)  
  
    -   O (Operator)  
  
    -   S (Source Name)  
  
    -   G (Source GUID)  
  
    -   X (Execution GUID)  
  
    -   M (Message)  
  
    -   T (Time Start and End)  
  
     Sono disponibili i valori *list_options* seguenti:  
  
    -   *I* - Specifica l'elenco di inclusione. Solo i nomi o i GUID delle origini specificati vengono registrati.  
  
    -   *E* - Specifica l'elenco di esclusione. I nomi o i GUID delle origini specificati non vengono registrati.  
  
    -   Il parametro *src_name_or_guid* specificato per inclusioni o esclusioni è un nome di evento o un nome o un GUID dell'origine.  
  
     Se nello stesso prompt dei comandi si usano più opzioni **/ConsoleLog** , queste interagiscono nel modo di seguito descritto:  
  
    -   L'ordine di visualizzazione non è significativo.  
  
    -   Se nella riga di comando non sono presenti elenchi di inclusioni, gli elenchi di esclusioni vengono applicati a tutti i tipi di voci di log.  
  
    -   Se nella riga di comando sono presenti elenchi di inclusione, all'unione di tutti gli elenchi di inclusione vengono applicati gli elenchi di esclusione.  
  
     Per esempi relativi all'opzione **/ConsoleLog** , vedere la sezione **osservazioni** .  
  
-   **/D[ts]** _package_path_:   
                  Facoltativa. Carica un pacchetto dall'archivio pacchetti SSIS. I pacchetti archiviati nell'archivio pacchetti SSIS vengono distribuiti tramite il modello di distribuzione del pacchetto legacy. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, utilizzare l'opzione `/ISServer`. Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [distribuzione di progetti e pacchetti](deploy-integration-services-ssis-projects-and-packages.md).  
  
     L'argomento *package_path* consente di specificare il percorso relativo del pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] a partire dalla radice dell'archivio pacchetti SSIS e include il nome del pacchetto [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Se nel percorso o nel nome file specificato nell'argomento *package_path* è contenuto uno spazio, è necessario racchiudere l'argomento *package_path* tra virgolette.  
  
     L'opzione `/DTS` non può essere utilizzata in combinazione con l'opzione `/File` o `/SQL`. Se si specificano più opzioni, l'esecuzione di `dtexec` avrà esito negativo.  
  
-   **/De [crypt]**  _password_: facoltativa. Consente di impostare la password di decrittografia utilizzata per caricare un pacchetto con password crittografata.  
  
-   **/Dump** _error code_:  
                  Facoltativo consente di creare i file di dump del debug, con estensione MDMP e tmp, quando si verificano uno o più eventi specificati durante l'esecuzione del pacchetto. L'argomento del *codice di errore* specifica il tipo di codice evento, ovvero errore, avviso o informazioni, che attiverà il sistema per creare i file di dump del debug. Per specificare più codici evento, separare ciascun argomento *error code* con un punto e virgola (;). Non includere virgolette con l'argomento *error code* .  
  
     Nell'esempio seguente vengono generati i file di dump del debug se si verifica l'errore DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     Per impostazione predefinita, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archivia i file di dump del debug nella cartella *\<drive>* : \Programmi\microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > [!NOTE]  
    >  I file di dump del debug possono contenere informazioni riservate. Utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato. Ad esempio, prima di inviare i file del debug al supporto tecnico Microsoft, si consiglia di rimuovere eventuali informazioni sensibili o riservate.  
  
     Per applicare questa opzione a tutti i pacchetti `dtexec` eseguiti dall'utilità, aggiungere un valore REG_SZ **DumpOnCodes** alla chiave del registro di sistema HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath.. Il valore dei dati in **DumpOnCodes** specifica il codice di errore o i codici che generano la creazione di file di dump del debug da parte del sistema. Più codici di errore devono essere separati da un punto e virgola (;).  
  
     Se si aggiunge un valore **DumpOnCodes** alla chiave del registro di sistema e si usa l'opzione **/Dump** , il sistema crea file di dump del debug basati su entrambe le impostazioni.  
  
     Per ulteriori informazioni sui file di dump del debug, vedere [generazione di file di dump per l'esecuzione del pacchetto](../troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**:   
                  Facoltativa. Consente di creare i file di dump del debug, con estensione MDMP e tmp, quando si verifica un errore durante l'esecuzione del pacchetto.  
  
     Per impostazione predefinita, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archivia i file di dump del debug nella cartella *\<drive>* : \Programmi\microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > [!NOTE]  
    >  I file di dump del debug possono contenere informazioni riservate. Utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato. Ad esempio, prima di inviare i file del debug al supporto tecnico Microsoft, si consiglia di rimuovere eventuali informazioni sensibili o riservate.  
  
     Per applicare questa opzione a tutti i pacchetti `dtexec` eseguiti dall'utilità, aggiungere un valore REG_DWORD **DumpOnError** alla chiave del registro di sistema HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath.. Il valore del valore del REG_DWORD **DumpOnError** determina se l'opzione **/DumpOnError** deve essere utilizzata con l' `dtexec` Utilità:  
  
    -   Un valore di dati diverso da zero indica che il sistema creerà file di dump del debug quando si verifica un errore, indipendentemente dal fatto che si usi l'opzione **/DumpOnError** con l' `dtexec` utilità.  
  
    -   Un valore di dati pari a zero indica che il sistema non creerà i file di dump del debug a meno che non si usi l'opzione **/DumpOnError** con l' `dtexec` utilità.  
  
     Per ulteriori informazioni sui file di dump del debug, vedere [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   `/Env[Reference]`*ID riferimento dell'ambiente*:   
                  Facoltativa. Specifica il riferimento all'ambiente (ID) utilizzato dall'esecuzione del pacchetto, per un pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Nei parametri configurati per l'associazione alle variabili verranno utilizzati i valori delle variabili contenuti nell'ambiente.  
  
     È possibile utilizzare l'opzione `/Env[Reference]` in combinazione con le opzioni `/ISServer` e `/Server`.  
  
     Questo parametro viene utilizzato da SQL Server Agent.  
  
-   **/F[ile]** _filespec_:   
                  Facoltativa. Carica un pacchetto salvato nel file system. I pacchetti salvati nel file system vengono distribuiti tramite il modello di distribuzione del pacchetto legacy. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, utilizzare l'opzione `/ISServer`. Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md).  
  
     L'argomento *filespec* specifica il percorso e il nome file del pacchetto. È possibile specificare il percorso in formato UNC (Universal Naming Convention) o come percorso locale. Se nel percorso o nel nome file specificato nell'argomento *filespec* è contenuto uno spazio, è necessario racchiudere l'argomento *filespec* tra virgolette.  
  
     L'opzione `/File` non può essere utilizzata in combinazione con l'opzione `/DTS` o `/SQL`. Se si specificano più opzioni, l'esecuzione di `dtexec` avrà esito negativo.  
  
-   **/H [ELP]** [*Option_name*]: facoltativo. Consente di visualizzare le informazioni della Guida relative alle opzioni o all'opzione specificata dall'argomento *option_name* e quindi di chiudere l'utilità.  
  
     Se si specifica un argomento di *option_name* , `dtexec` viene avviata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la documentazione online di e viene visualizzato l'argomento relativo all'utilità dtexec.  
  
-   `/ISServer`*PackagePath*:  
                  Facoltativa. Esegue un pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Con l'argomento *PackagePath* vengono specificati il percorso completo e il nome file del pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se il percorso o il nome file specificato nell'argomento *PackagePath* contiene uno spazio, è necessario racchiudere l'argomento *PackagePath* tra virgolette.  
  
     Il formato del pacchetto è il seguente:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     È possibile utilizzare l'opzione `/Server` in combinazione con l'opzione `/ISSERVER`. Un pacchetto nel server SSIS può essere eseguito solo con l'autenticazione di Windows. Per accedere al pacchetto viene utilizzato l'utente corrente di Windows. Se si omette l'opzione /Server, viene usata l'istanza locale predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     L'opzione `/ISSERVER` non può essere utilizzata in combinazione con l'opzione `/DTS`, `/SQL` o `/File`. Se si specificano più opzioni, l'esecuzione di dtexec avrà esito negativo.  
  
     Questo parametro viene utilizzato da SQL Server Agent.  
  
-   **/L[ogger]** _classid_orprogid;configstring_:  
                  Facoltativa. Associa uno o più provider di log all'esecuzione di un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Il parametro *classid_orprogid* specifica il provider di log e può essere specificato come un GUID di classe. L'argomento *configstring* è la stringa utilizzata per configurare il provider di log.  
  
     Di seguito sono elencati i provider di log disponibili:  
  
    -   File di testo  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Registro eventi di Windows  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   File XML  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** _concurrent_executables_:  
                  Facoltativa. Consente di specificare il numero di file eseguibili che il pacchetto è in grado di eseguire contemporaneamente. Il valore specificato deve essere un valore intero non negativo oppure -1. Il valore -1 indica che [!INCLUDE[ssIS](../../includes/ssis-md.md)] supporta un numero massimo di file eseguibili in esecuzione simultanea uguale al numero totale di processori nel computer in cui è eseguito il pacchetto, più due.  
  
-   **/Pack[age]** _PackageName_:  
                  Facoltativa. Specifica il pacchetto che viene eseguito. Questo parametro viene utilizzato principalmente quando si esegue il pacchetto da [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   **/P [assword]** _password_:  
                  Facoltativa. Consente il recupero di un pacchetto protetto tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione viene usata in combinazione con l'opzione **/User** . Se si omette l'opzione **/Password** e viene usata l'opzione **/User** , verrà usata una password vuota. Il valore di *password* può essere racchiuso tra virgolette.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par [ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)]; *literal_value*: facoltativo. Specifica i valori dei parametri. È possibile specificare più opzioni **/Parameter** . I tipi di dati sono CLR TypeCodes come stringhe. Per un parametro non stringa, il tipo di dati viene specificato in parentesi, dopo il nome del parametro.  
  
     L'opzione **/Parameter** può essere usata solo con l' `/ISServer` opzione.  
  
     È possibile utilizzare i prefissi $Package, $Project e $ServerOption per indicare rispettivamente un parametro di pacchetto, un parametro di progetto e un parametro di opzione server. Il pacchetto è il tipo di parametro predefinito.  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto e all'impostazione di myvalue per il parametro di progetto (myparam) e del valore intero 12 per il parametro di pacchetto (anotherparam).  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     È inoltre possibile impostare le proprietà di gestione connessione utilizzando i parametri. Per identificare un parametro di gestione connessione utilizzare il prefisso CM.  
  
     Nell'esempio seguente la proprietà InitialCatalog della gestione connessione SourceServer è impostata su `ssisdb`.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     Nell'esempio seguente la proprietà ServerName della gestione connessione SourceServer è impostata su un punto (.) per indicare il server locale.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** _ProjectFile_:  
                  Facoltativa. Specifica il progetto da cui recuperare il pacchetto che viene eseguito. Con l'argomento *ProjectFile* viene specificato il nome file con estensione ispac. Questo parametro viene utilizzato principalmente quando si esegue il pacchetto da [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
-   **/Rem** _comment_:  
                  Facoltativa. Include i commenti nel prompt dei comandi o nei file di comando. L'argomento è facoltativo. Il valore di *comment* è una stringa che deve essere racchiusa tra virgolette o non deve contenere spazi. Se non si specifica alcun argomento, viene inserita una riga vuota. Durante la fase di determinazione dell'origine del comando, i valori*comment* vengono eliminati.  
  
-   **/Rep [orting]** _level_ [*; event_guid_or_name*[*; event_guid_or_name*[...]]: facoltativo. Specifica i tipi di messaggi da segnalare. Le opzioni relative alle opzioni per *level* sono elencate di seguito:  
  
     **N** Nessun report.  
  
     `E`Vengono segnalati errori.  
  
     **W** Gli avvisi vengono segnalati.  
  
     `I`Vengono segnalati messaggi informativi.  
  
     **C** Gli eventi personalizzati vengono segnalati.  
  
     **D** Gli eventi relativi alle attività Flusso di dati vengono segnalati.  
  
     **P** Lo stato viene segnalato.  
  
     **V** Report dettagliati.  
  
     Gli argomenti V e N escludono tutti gli altri argomenti e pertanto devono essere specificati da soli. Se l'opzione **/Reporting** non è specificata, il livello predefinito è `E` (Errors), **W** (warnings) e **P** (Progress).  
  
     Tutti gli eventi sono preceduti da un timestamp nel formato "AA/MM/GG HH:MM:SS" e da un GUID o un nome descrittivo se disponibile.  
  
     Il parametro facoltativo *event_guid_or_name* è un elenco di eccezioni per i provider di log. ovvero gli eventi da non registrare che potrebbero altrimenti essere stati registrati.  
  
     Non è necessario escludere un evento se normalmente non viene registrato per impostazione predefinita.  
  
-   **/Res [Tart]** {*Deny | Force | IfPossible*}: facoltativo. Specifica un nuovo valore per la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> nel pacchetto. Di seguito è descritto il significato di ogni parametro.  
  
     *Deny* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Force* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     Se non si specifica alcun valore, viene usato il valore predefinito **force** .  
  
-   **/Set** [$sensitive::]*PropertyPath; value*: facoltativo. Ignora la configurazione di un parametro, una variabile, una proprietà, un contenitore, un provider di log, un enumeratore Foreach o una connessione all'interno di un pacchetto. Se si specifica questa opzione, **/Set** modifica il valore dell'argomento *propertyPath* nel valore specificato. È possibile specificare più opzioni **/Set** .  
  
     Oltre a usare l'opzione **/set** con l'opzione **/f [ile]** , è anche possibile usare l'opzione **/set** con l'opzione `/ISServer` o `/Project` . Quando si usa **/set** con `/Project` , **/set** imposta i valori dei parametri. Quando si usa **/set** con `/ISServer` , **/set** imposta gli override delle proprietà. Inoltre, quando si utilizza **/set** con `/ISServer` , è possibile utilizzare il prefisso $sensitive facoltativo per indicare che la proprietà deve essere considerata sensibile nel [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Server.  
  
     È possibile determinare il valore di *propertyPath* eseguendo la Configurazione guidata pacchetto. I percorsi per gli elementi selezionati vengono visualizzati nella pagina finale **Completamento procedura guidata** e possono essere copiati e incollati. Se si utilizza la procedura guidata soltanto a questo scopo, è possibile annullare la procedura guidata dopo aver copiato i percorsi.  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto salvato nel file system e all'impostazione di un nuovo valore per una variabile:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto dal file di progetto con estensione ispac e all'impostazione dei parametri di pacchetto e di progetto.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     È possibile usare l'opzione **/Set** per modificare il percorso da cui vengono caricate le configurazioni di pacchetto. Non è tuttavia possibile usare l'opzione **/Set** per ignorare un valore specificato da una configurazione in fase di progettazione. Per comprendere il modo in cui vengono applicate le configurazioni dei pacchetti, vedere [configurazioni di pacchetto](../package-configurations.md) e [modifiche del comportamento per le funzionalità Integration Services di SQL Server 2014](../behavior-changes-to-integration-services-features-in-sql-server-2014.md).  
  
-   `/Ser[ver]`*Server*:  
                  Facoltativa. Se si specifica l'opzione `/SQL` o `/DTS`, questa opzione specifica il nome del server dal quale recuperare il pacchetto. Se si omette l'opzione `/Server` e si specifica l'opzione `/SQL` o `/DTS`, verrà tentata l'esecuzione del pacchetto nel server locale. Il valore *server_instance* può essere racchiuso fra virgolette.  
  
     L'opzione `/Ser[ver]` è obbligatoria se è specificata l'opzione `/ISServer`.  
  
-   **/SQ[L]** _package_path_:  
                  Carica un pacchetto archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database `msdb`. I pacchetti archiviati nel database `msdb` vengono distribuiti tramite il modello di distribuzione del pacchetto. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, utilizzare l'opzione `/ISServer`. Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [distribuzione di progetti e pacchetti](deploy-integration-services-ssis-projects-and-packages.md).  
  
     Con l'argomento *package_path* viene specificato il nome del pacchetto da recuperare. Se nel percorso vengono incluse cartelle, queste sono seguite da una barra rovesciata ("\\"). Il valore *package_path* può essere racchiuso fra virgolette. Se nel percorso o nel nome file specificato nell'argomento *package_path* è contenuto uno spazio, è necessario racchiudere l'argomento *package_path* tra virgolette.  
  
     È possibile usare le opzioni **/User**, **/password**e `/Server` con l' `/SQL` opzione.  
  
     Se si omette l'opzione **/User** , per accedere al pacchetto verrà usata l'autenticazione di Windows. Se si usa l'opzione **/User** , il nome dell'account di accesso **/User** specificato viene associato all'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     L'opzione **/Password** viene usata solo in combinazione con l'opzione **/User** . Se si usa l'opzione **/Password** , l'accesso al pacchetto avviene in base alle informazioni sul nome utente e sulla password specificate. Se si omette l'opzione **/Password** , verrà usata una password vuota.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
     Se si omette l'opzione `/Server`, viene utilizzata l'istanza locale predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     L'opzione `/SQL` non può essere utilizzata in combinazione con l'opzione `/DTS` o `/File`. Se si specificano più opzioni, l'esecuzione di `dtexec` avrà esito negativo.  
  
-   **/Su [m]**: facoltativo. Consente di visualizzare un contatore incrementale con il numero di righe che verranno ricevute dal componente successivo.  
  
-   **/U [ser]** _user_name_:  
                  Facoltativa. Consente il recupero di un pacchetto protetto tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione viene utilizzata solo se si specifica l'opzione `/SQL`. Il valore *user_name* può essere racchiuso tra virgolette.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va [lidate]**:  
                  Facoltativa. Consente di arrestare l'esecuzione del pacchetto dopo la fase di convalida, quindi il pacchetto non viene eseguito. Durante la convalida, l'uso dell'opzione **/warnaserror** fa `dtexec` in modo che consideri un avviso come un errore, pertanto il pacchetto ha esito negativo se si verifica un avviso durante la convalida.  
  
-   **/VerifyB [uild]** _Major_[*; minor*[*; Build*]]: facoltativo. Consente di verificare il numero di build di un pacchetto rispetto ai numeri di build specificati durante la fase di verifica negli argomenti *major*, *minor*e *build* . Se i numeri non corrispondono, il pacchetto non verrà eseguito.  
  
     I valori sono di tipo integer long. L'argomento può avere uno dei tre formati seguenti. Il valore *major* è sempre obbligatorio:  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** _packageID_:  
                  Facoltativa. Consente di verificare il GUID del pacchetto da eseguire in base al valore specificato nell'argomento *package_id* .  
  
-   **/VerifyS[igned]**:  
                  Facoltativa. Comporta il controllo della firma digitale del pacchetto da parte di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se il pacchetto non è firmato o se la firma non è valida, il pacchetto ha esito negativo. Per altre informazioni, vedere [Identificazione dell'origine dei pacchetti con firme digitali](../security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > [!IMPORTANT]  
    >  Se [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è configurato per la verifica della firma del pacchetto, gli unici controlli che vengono eseguiti sono quelli relativi alla presenza e alla validità della firma digitale, nonché all'attendibilità dell'origine. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non controlla se il pacchetto è stato modificato.  
  
    > [!NOTE]  
    >  Il valore facoltativo del registro di sistema **BlockedSignatureStates** può specificare un'impostazione più restrittiva rispetto all'opzione per la firma digitale impostata in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] o nella riga di `dtexec` comando. In questo caso, l'impostazione del Registro di sistema più restrittiva ha la precedenza rispetto ad altre impostazioni.  
  
-   **/VerifyV [ersionID]** _VersionId_: facoltativa. Consente di verificare il GUID di versione di un pacchetto da eseguire in base al valore specificato nell'argomento *version_id* durante la fase di convalida del pacchetto.  
  
-   **/VLog** _[filespec]_: facoltativo. Consente di scrivere tutti gli eventi dei pacchetti Integration Services nei provider di log abilitati durante la progettazione del pacchetto. Per consentire l'abilitazione di un provider di log per i file di testo e la scrittura degli eventi del log in un file di testo specifico, includere un percorso e un nome file come parametro *Filespec* .  
  
     Se non si include il parametro *Filespec* , non sarà possibile abilitare un provider di log per i file di testo. Gli eventi del log verranno scritti solo nei provider di log abilitati durante la progettazione del pacchetto.  
  
-   **/W [arnAsError]**:  
                  Facoltativa. Poiché un avviso viene interpretato come un errore, il pacchetto non viene eseguito se durante la convalida viene generato un avviso. Se non viene generato alcun avviso durante la convalida e si omette l'opzione **/Validate** , il pacchetto viene eseguito.  
  
-   **/X86**: facoltativo. Determina l'esecuzione del pacchetto in modalità a 32 bit in un computer a 64 bit da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa opzione viene impostata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando sono soddisfatte le condizioni seguenti:  
  
    -   Il tipo di passaggio del processo è **Pacchetto SQL Server Integration Services**.  
  
    -   L'opzione **Usa runtime a 32 bit** nella scheda **Opzioni di esecuzione** della finestra di dialogo **Nuovo passaggio di processo** è selezionata.  
  
     È anche possibile impostare questa opzione per un passaggio del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando le stored procedure o SQL Server Management Objects (SMO) per creare il processo a livello di codice.  
  
     Questa opzione è utilizzata solo da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa opzione viene ignorata se si esegue l'utilità `dtexec` dal prompt dei comandi.  
  
##  <a name="remarks"></a>Osservazioni su <a name="remark"></a>  
 L'ordine in cui vengono specificate le opzioni del comando può influire sulla modalità di esecuzione del pacchetto:  
  
-   Le opzioni vengono elaborate nell'ordine che occupano nella riga di comando. I file di comando vengono letti in base all'ordine con cui vengono rilevati nella riga di comando, in modo analogo ai comandi nel file di comando.  
  
-   Se la stessa opzione, lo stesso parametro o la stessa variabile compare più volte nella stessa istruzione della riga di comando, l'ultima istanza dell'opzione avrà la precedenza sulle altre.  
  
-   Le opzioni **/Set** e **/ConfigFile** vengono elaborate nell'ordine in cui vengono rilevate.  
  
##  <a name="examples"></a><a name="example"></a> Esempi  
 Gli esempi seguenti illustrano come usare l' `dtexec` utilità del prompt dei comandi per configurare ed eseguire i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti.  
  
 **Esecuzione di pacchetti**  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di Windows, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nella cartella del file system nell'archivio pacchetti SSIS, utilizzare il codice seguente:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Per convalidare un pacchetto che utilizza l'autenticazione di Windows ed è salvato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza tuttavia eseguirlo, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system e per specificare le opzioni di registrazione, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Per eseguire un pacchetto che utilizza l'autenticazione di Windows ed è salvato nell'istanza predefinita locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e verificarne la versione prima della sua esecuzione, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system e configurato esternamente, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> [!NOTE]  
>  Gli argomenti *package_path* o *filespec* delle opzioni /SQL, /DTS o /FILE devono essere racchiusi tra virgolette se il percorso o il nome del file contiene uno spazio. Se non è racchiuso tra virgolette, un argomento non può contenere spazi vuoti.  
  
 **Opzioni di registrazione**  
  
 Si supponga, ad esempio, che i tipi di voci di log siano A, B e C. Nell'esempio seguente l'opzione **ConsoleLog** senza alcun parametro visualizza tutti e tre i tipi di log con tutti i campi:  
  
```  
/CONSOLELOG  
```  
  
 Nell'opzione seguente vengono visualizzati tutti i tipi di log, ma solo con le colonne Name e Message:  
  
```  
/CONSOLELOG NM  
```  
  
 Nell'opzione seguente vengono visualizzate tutte le colonne, ma solo per il tipo di voce di log A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 Nell'opzione seguente viene visualizzato solo il tipo di voce di log A con le colonne Name e Message:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 L'opzione seguente consente di visualizzare le voci di log per i tipi di voci di log A e B:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 È possibile ottenere gli stessi risultati usando più opzioni **ConsoleLog** :  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Se l'opzione **ConsoleLog** viene usata senza parametri, vengono visualizzati tutti i campi. L'inclusione di un parametro *list_options* comporta la visualizzazione solo del tipo di voce di log A con tutti i campi:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 L'esempio seguente visualizza tutte le voci di log eccetto il tipo di voce di log A, ovvero visualizza i tipi di voce di log B e C:  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 Nell'esempio seguente gli stessi risultati vengono ottenuti usando più opzioni **ConsoleLog** e una singola esclusione:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 Nell'esempio seguente non viene visualizzato alcun messaggio di log poiché, quando un tipo di file di log si trova sia nell'elenco delle inclusioni sia in quello delle esclusioni, esso verrà escluso.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Opzione SET**  
  
 L'esempio seguente illustra come usare l'opzione **/SET** tramite cui è possibile modificare il valore di qualsiasi variabile o proprietà del pacchetto quando si avvia il pacchetto dalla riga di comando.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Opzione Project**  
  
 L'esempio seguente illustra come usare le opzioni `/Project` e `/Package`.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 Nell'esempio seguente si illustra come utilizzare le opzioni `/Project` e `/Package` e come impostare i parametri del pacchetto e del progetto.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **Opzione ISServer**  
  
 L'esempio seguente illustra come usare l'opzione `/ISServer`.  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 Nell'esempio seguente si illustra come utilizzare l'opzione `/ISServer` e come impostare i parametri del progetto e di gestione connessione.  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-tasks"></a>Attività correlate  
 [Eseguire un pacchetto in SQL Server Data Tools](../run-a-package-in-sql-server-data-tools.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento sul blog relativo a [codici di uscita, DTEXEC e catalogo SSIS](https://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/), su www.mattmasson.com.  
  
  
