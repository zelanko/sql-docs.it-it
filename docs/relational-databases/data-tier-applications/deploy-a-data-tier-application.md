---
title: Distribuire un'applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 842a6519c1493162d06c853f11a9494d8dc3ca5b
ms.sourcegitcommit: ba44730f5cc33295ae2ed1f281186dd266bad4ef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/19/2019
ms.locfileid: "74190124"
---
# <a name="deploy-a-data-tier-application"></a>Distribuire un'applicazione livello dati
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile distribuire un'applicazione livello dati (DAC) da un pacchetto di applicazione livello dati a un'istanza esistente del motore di database o del database SQL di Azure usando una procedura guidata o uno script di PowerShell. 
  
 Il processo di distribuzione registra un'istanza di applicazione livello dati archiviando la definizione dell'applicazione livello dati nel database di sistema **msdb** (**master** in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]), crea un database e quindi lo popola con tutti gli oggetti di database definiti nell'applicazione livello dati.  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>Distribuire più volte lo stesso pacchetto di applicazione livello dati 
 È possibile distribuire più volte lo stesso pacchetto di applicazione livello dati in una sola istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)], ma le distribuzioni devono essere eseguite una alla volta. Il nome dell'istanza di applicazione livello dati specificato per ogni distribuzione deve essere univoco all'interno dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Se si distribuisce un'applicazione livello dati in un'istanza del motore di database, l'applicazione livello dati distribuita viene incorporata in **Utilità SQL Server** al successivo invio del set di raccolta dell'utilità dall'istanza al punto di controllo dell'utilità. L'applicazione livello dati sarà quindi presente nel nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** e segnalata nella pagina dei dettagli **Deployed Data-tier Applications** (Applicazioni livello dati distribuite).  
  
###  <a name="database-options-and-settings"></a>Opzioni e impostazioni del database  
 Per impostazione predefinita, il database creato durante la distribuzione disporrà di tutte le impostazioni predefinite incluse nell'istruzione CREATE DATABASE, fatta eccezione per le seguenti:  
  
-   Le regole di confronto e il livello di compatibilità del database sono impostati sui valori definiti nel pacchetto di applicazione livello dati. I pacchetti di applicazione livello dati compilati da un progetto di database in SQL Server Developer Tools usano i valori impostati nel progetto di database. I pacchetti estratti da un database esistente usano i valori del database originale.  
  
-   È possibile modificare alcune delle impostazioni del database, ad esempio il nome del database e i percorsi di file, nella pagina **Aggiorna configurazione** . Non è possibile impostare i percorsi dei file durante la distribuzione in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Alcune opzioni del database, ad esempio TRUSTWORTHY, DB_CHAINING e HONOR_BROKER_PRIORITY, non possono essere modificate durante il processo di distribuzione. Le proprietà fisiche, ad esempio il numero di filegroup o i numeri e le dimensioni dei file, non possono essere modificate durante il processo di distribuzione. Al termine della distribuzione, è possibile usare l'istruzione ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell per modificare il database in base alle proprie esigenze.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 È possibile distribuire un'applicazione livello dati a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], o un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che esegue [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o versioni successive. Se si crea un'applicazione livello dati usando una versione successiva, è possibile che nell'applicazione in questione siano contenuti oggetti non supportati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Non è possibile distribuire tali applicazioni livello dati a istanze di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
    
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni
Gli account di accesso dell'autenticazione vengono archiviati in un pacchetto di applicazione livello dati senza password. Quando il pacchetto viene distribuito o aggiornato, l'account di accesso viene creato come account disabilitato con una password generata. Per abilitare gli account di accesso, è necessario accedere usando un account con l'autorizzazione ALTER ANY LOGIN e usare ALTER LOGIN per abilitare l'account di accesso e assegnare una nuova password che può essere comunicata all'utente. Questa operazione non è necessaria per gli account di accesso dell'autenticazione di Windows, in quanto le relative password non sono gestite da SQL Server.  
  
 Un'applicazione livello dati può essere distribuita unicamente dai membri del ruolo predefinito del server **sysadmin** o **serveradmin** oppure tramite gli account di accesso disponibili nel ruolo predefinito del server **dbcreator** con autorizzazioni ALTER ANY LOGIN. È anche possibile distribuire un'applicazione livello dati usando l'account amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito denominato **sa** . 

La distribuzione di un'applicazione livello dati con accessi in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] richiede l'appartenenza ai ruoli loginmanager o serveradmin. Per la distribuzione di un'applicazione livello dati senza account di accesso in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesta l'appartenenza ai ruoli dbmanager o serveradmin.  
  
## <a name="deploy-a-dac-using-the-wizard"></a>Distribuire un'applicazione livello dati tramite una procedura guidata  
  
1.  In **Esplora oggetti**espandere il nodo per le istanze a cui si desidera distribuire l'applicazione livello dati.  
  
2.  Fare clic con il pulsante destro del mouse sul nodo **Database** e quindi selezionare **Distribuisci applicazione livello dati**.  
  
3.  Completare le finestre di dialogo della procedura guidata e fare clic su Fine.

Di seguito sono disponibili altre informazioni su alcune delle pagine della procedura guidata: 
     
### <a name="select-dac-package-page"></a>Pagina Selezione pacchetto di applicazione livello dati  
 Specificare il pacchetto di applicazione livello dati contenente l'applicazione livello dati da distribuire. La pagina passa attraverso tre stati.  
    
### <a name="select-the-dac-package"></a>Selezionare pacchetto di applicazione livello dati  
 Scegliere il pacchetto di applicazione livello dati da distribuire. È necessario specificare un file di pacchetto di applicazione livello dati valido con estensione dacpac.  
  
 **Pacchetto di applicazione livello dati** : consente di specificare il percorso e il nome file del pacchetto di applicazione livello dati contenente l'applicazione livello dati da distribuire. Per passare al percorso del pacchetto di applicazione livello dati, è possibile fare clic sul pulsante **Sfoglia** a destra della casella.  
  
 **Nome applicazione** casella di sola lettura in cui viene visualizzato il nome dell'applicazione livello dati assegnato durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Versione** casella di sola lettura in cui viene visualizzata la versione assegnata durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Descrizione**: casella di sola lettura in cui viene visualizzata la descrizione immessa durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
### <a name="validating-the-dac-package"></a>Convalida del pacchetto di applicazione livello dati  
 Viene visualizzato un indicatore di stato per la verifica della validità del file selezionato come pacchetto di applicazione livello dati. Se il pacchetto di applicazione livello dati viene convalidato, la procedura guidata continua con la versione finale della pagina **Seleziona pacchetto** in cui è possibile controllare il risultato della convalida. Se il file non è un pacchetto di applicazione livello dati valido, rimane visualizzata la pagina **Selezione pacchetto di applicazione livello dati**. Selezionare un altro pacchetto di applicazione livello dati valido o annullare la procedura guidata e generare un nuovo pacchetto di applicazione livello dati.  
  
  ### <a name="review-policy-page"></a>Pagina Verifica criteri  
 Controllare i risultati della valutazione degli eventuali criteri di selezione dei server dell'applicazione livello dati. I criteri di selezione dei server del pacchetto di applicazione livello dati sono facoltativi e sono assegnati al pacchetto di applicazione livello dati quando viene creato in Visual Studio. I facet dei criteri di selezione dei server vengono usati per specificare le condizioni che un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve soddisfare per ospitare il pacchetto DAC.  
  
 **Risultati della valutazione delle condizioni dei criteri**: indica se le condizioni dei criteri di distribuzione dell'applicazione livello dati sono soddisfatte. I risultati della valutazione di ogni condizione sono riportati in una riga distinta.  
  
 I criteri di selezione dei server riportati di seguito vengono valutati sempre come falsi durante la distribuzione di un'applicazione livello dati a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: versione del sistema operativo, lingua, Named Pipes abilitato, piattaforma e tcp abilitato.  
  
 **Ignora le violazioni dei criteri** : usare questa casella di controllo per continuare la distribuzione se una o più delle condizioni dei criteri non sono soddisfatte. Selezionare questa opzione solo se si è sicuri che tutte le condizioni non soddisfatte non impediranno la distribuzione del pacchetto DAC.  
   
### <a name="update-configuration-page"></a>Pagina Aggiorna configurazione  
 Specificare i nomi dell'istanza di applicazione livello dati distribuita e del database creato dalla distribuzione e impostare le opzioni del database.  
  
 **Nome database** : consente di specificare il nome del database da creare con la distribuzione. Il nome predefinito corrisponde al nome del database di origine da cui è stato estratto il pacchetto di applicazione livello dati. Il nome deve essere univoco all'interno dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ed essere conforme alle regole per gli identificatori del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Se si modifica il nome del database, i nomi del file di dati e del file di log verranno modificati in modo da corrispondere al nuovo valore.  
  
 Il nome del database viene inoltre usato come nome dell'istanza di applicazione livello dati. Il nome dell'istanza è visualizzato nel nodo dell'applicazione livello dati, nel nodo **Applicazioni livello dati** in **Esplora oggetti**o nel nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in **Esplora utilità**.  
  
 Le opzioni seguenti non si applicano a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]e non vengono visualizzate in caso di distribuzione in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Usa percorso predefinito file di database** : selezionare questa opzione per creare i file di dati e di log del database nel percorso predefinito per l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. I nomi dei file saranno creati usando il nome del database.  
  
 **Specifica file di database** : selezionare questa opzione per specificare un percorso o un nome diverso per i file di dati e di log.  
  
 **Percorso e nome file di dati** : consente di specificare il percorso completo e il nome del file di dati. La casella viene popolata con il percorso e il nome file predefiniti. Modificare la stringa nella casella per modificare l'impostazione predefinita oppure usare il pulsante Sfoglia per passare alla cartella in cui si desidera salvare il file di dati.  
  
 **Percorso e nome file di log** : consente di specificare il percorso completo e il nome del file di log. La casella viene popolata con il percorso e il nome file predefiniti. Modificare la stringa nella casella per modificare l'impostazione predefinita oppure usare il pulsante **Sfoglia** per passare alla cartella in cui si desidera salvare il file di log.  
  
###  <a name="Summary"></a> Pagina Riepilogo  
 Usare questa pagina per controllare le azioni che verranno eseguite dalla procedura guidata durante la distribuzione del pacchetto di applicazione livello dati.  
  
 **Le impostazioni seguenti saranno usate per implementare l'applicazione livello dati.** Controllare le informazioni visualizzate per assicurarsi che le azioni che verranno eseguite siano corrette. Nella finestra viene visualizzato il pacchetto di applicazione livello dati selezionato e il nome selezionato per l'istanza di applicazione livello dati distribuita. Nella finestra vengono inoltre visualizzate le impostazioni che verranno usate durante la creazione del database associato al pacchetto di applicazione livello dati.  
   
### <a name="deploy-page"></a>Pagina Distribuisci  
 In questa pagina viene segnalato l'esito positivo o negativo dell'operazione di distribuzione.  
  
 **Distribuzione dell'applicazione livello dati** : consente di visualizzare l'esito positivo o negativo di ogni azione eseguita per distribuire l'applicazione livello dati. Verificare le informazioni che determinano l'esito positivo o negativo di ciascuna azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Selezionare il collegamento per visualizzare un report dell'errore per l'azione.  
  
 **Salva report** : consente di salvare il report della distribuzione come file HTML. Nel file viene riportato lo stato di ogni azione, inclusi tutti gli errori generati da qualsiasi azione. La cartella predefinita è la cartella SQL Server Management Studio\DAC Packages contenuta nella cartella Documenti dell'account di Windows.  
  
  
##  <a name="using-powershell"></a>Utilizzo di PowerShell  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza a cui distribuire l'applicazione livello dati.  
  
2.  Aprire un oggetto **ServerConnection** e connetterlo alla stessa istanza.  
  
3.  Usare **System.IO.File** per caricare il file del pacchetto di applicazione livello dati.  
  
4.  Usare **add_DacActionStarted** e **add_DacActionFinished** per sottoscrivere gli eventi di distribuzione dell'applicazione livello dati.  
  
5.  Impostare **DatabaseDeploymentProperties**.  
  
6.  Usare il metodo **DacStore.Install** per distribuire l'applicazione livello dati.  
  
7.  Chiudere il flusso di file usato per leggere il file del pacchetto di applicazione livello dati.  

Nel seguente esempio viene distribuita un'applicazione livello dati denominata MyApplication su un'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)], usando una definizione dell'applicazione livello dati in un pacchetto MyApplication.dacpac.  
  
## <a name="powershell-examples"></a>Esempi di PowerShell  

Nel seguente esempio viene distribuita un'applicazione livello dati denominata MyApplication su un'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)], usando una definizione dell'applicazione livello dati in un pacchetto MyApplication.dacpac.  

```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverConnection,$dacName)  
$dacStore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>Ulteriori informazioni 
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Estrarre un'applicazione livello dati da un database](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [Identificatori del database](../../relational-databases/databases/database-identifiers.md)  
  
  
