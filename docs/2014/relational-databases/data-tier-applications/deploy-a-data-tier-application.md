---
title: Distribuire un'applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploydacwizard.updateconfiguration.f1
- sql12.swb.deploydacwizard.selectdac.f1
- sql12.swb.deploydacwizard.deploydac.f1
- sql12.swb.deploydacwizard.introduction.f1
- sql12.swb.deploydacwizard.summary.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2344ff0b95e82bd83e801df9ff6bd60328a2ae33
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970289"
---
# <a name="deploy-a-data-tier-application"></a>Distribuire un'applicazione livello dati
  È possibile distribuire un'applicazione livello dati (DAC) da un pacchetto di applicazione livello dati all'istanza esistente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usando una procedura guidata o uno script di PowerShell. Il processo di distribuzione registra un'istanza di applicazione livello dati archiviando la definizione dell'applicazione livello dati nel database di sistema **msdb** (**master** in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]), crea un database e quindi lo popola con tutti gli oggetti di database definiti nell'applicazione livello dati.  
  
-   **Prima di iniziare:**  [Utilità SQL Server](#SQLUtility), [Opzioni e impostazioni del database](#DBOptSettings), [Limitazioni e restrizioni](#LimitationsRestrictions), [Prerequisiti](#Prerequisites), [Sicurezza](#Security), [Autorizzazioni](#Permissions)  
  
-   **Per distribuire un'applicazione livello dati, usando:**  [procedura guidata Distribuisci applicazione livello dati](#UsingDeployDACWizard), [PowerShell](#DeployDACPowerShell)  
  
##  <a name="before-you-begin"></a><a name="BeforeBegin"></a> Prima di iniziare  
 È possibile distribuire più volte lo stesso pacchetto di applicazione livello dati in una sola istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , le distribuzioni devono, tuttavia, essere eseguite una alla volta. Il nome dell'istanza di applicazione livello dati specificato per ogni distribuzione deve essere univoco all'interno dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
###  <a name="sql-server-utility"></a><a name="SQLUtility"></a>Utilità SQL Server  
 Se si distribuisce un'applicazione livello dati in un'istanza gestita del Motore di database, il pacchetto di applicazione livello dati distribuito viene incorporato in Utilità SQL Server al successivo invio del set di raccolta dell'utilità dall'istanza al punto di controllo dell'utilità. L'applicazione livello dati sarà quindi presente nel nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** e segnalata nella pagina dei dettagli **Deployed Data-tier Applications** (Applicazioni livello dati distribuite).  
  
###  <a name="database-options-and-settings"></a><a name="DBOptSettings"></a>Opzioni e impostazioni del database  
 Per impostazione predefinita, il database creato durante la distribuzione disporrà di tutte le impostazioni predefinite incluse nell'istruzione CREATE DATABASE, fatta eccezione per le seguenti:  
  
-   Le regole di confronto e il livello di compatibilità del database sono impostati sui valori definiti nel pacchetto di applicazione livello dati. I pacchetti di applicazione livello dati compilati da un progetto di database in SQL Server Developer Tools usano i valori impostati nel progetto di database. I pacchetti estratti da un database esistente usano i valori del database originale.  
  
-   È possibile modificare alcune delle impostazioni del database, ad esempio il nome del database e i percorsi di file, nella pagina **Aggiorna configurazione** . Non è possibile impostare i percorsi dei file durante la distribuzione in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Alcune opzioni del database, ad esempio TRUSTWORTHY, DB_CHAINING e HONOR_BROKER_PRIORITY, non possono essere modificate durante il processo di distribuzione. Le proprietà fisiche, ad esempio il numero di filegroup o i numeri e le dimensioni dei file, non possono essere modificate durante il processo di distribuzione. Al termine della distribuzione, è possibile usare l'istruzione ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell per modificare il database in base alle proprie esigenze.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 È possibile distribuire un'applicazione livello dati a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], o un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che esegue [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o versioni successive. Se si crea un'applicazione livello dati usando una versione successiva, è possibile che nell'applicazione in questione siano contenuti oggetti non supportati da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Non è possibile distribuire tali applicazioni livello dati a istanze di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 È consigliabile evitare di distribuire un pacchetto di applicazione livello dati proveniente da origini sconosciute o non attendibili. Tali pacchetti possono contenere codice dannoso che potrebbe eseguire codice indesiderato Transact-SQL o causare errori modificando lo schema. Prima di usare un pacchetto proveniente da un'origine sconosciuta o non attendibile, decomprimerlo e controllare il codice, ad esempio le stored procedure o altro codice definito dall'utente. Per altre informazioni su come eseguire questi controlli, vedere [Validate a DAC Package](validate-a-dac-package.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per migliorare la sicurezza, gli account di accesso dell'autenticazione di SQL Server vengono archiviati in un pacchetto di applicazione livello dati senza password. Quando il pacchetto viene distribuito o aggiornato, l'account di accesso viene creato come account disabilitato con una password generata. Per abilitare gli account di accesso, è necessario accedere usando un account che dispone dell'autorizzazione ALTER ANY LOGIN e usare ALTER LOGIN per abilitare l'account di accesso e assegnare una nuova password che può essere comunicata all'utente. Questa operazione non è necessaria per gli account di accesso dell'autenticazione di Windows, in quanto le relative password non sono gestite da SQL Server.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Un'applicazione livello dati può essere distribuita unicamente dai membri del ruolo predefinito del server **sysadmin** o **serveradmin** oppure tramite gli account di accesso disponibili nel ruolo predefinito del server **dbcreator** con autorizzazioni ALTER ANY LOGIN. È anche possibile distribuire un'applicazione livello dati usando l'account amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito denominato **sa** . La distribuzione di un'applicazione livello dati con accessi in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] richiede l'appartenenza ai ruoli loginmanager o serveradmin. Per la distribuzione di un'applicazione livello dati senza account di accesso in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesta l'appartenenza ai ruoli dbmanager o serveradmin.  
  
##  <a name="using-the-deploy-data-tier-application-wizard"></a><a name="UsingDeployDACWizard"></a>Utilizzo della procedura guidata Distribuisci applicazione livello dati  
 **Per distribuire un'applicazione livello dati tramite una procedura guidata**  
  
1.  In **Esplora oggetti**espandere il nodo per le istanze a cui si desidera distribuire l'applicazione livello dati.  
  
2.  Fare clic con il pulsante destro del mouse sul nodo **database** , quindi scegliere **Distribuisci applicazione livello dati...**  
  
3.  Completare le finestre di dialogo della procedura guidata.  
  
    -   [Pagina Introduzione](#Introduction)  
  
    -   [Pagina Selezione pacchetto di applicazione livello dati](#Select_dac_package)  
  
    -   [Pagina Verifica criteri](#Review_policy)  
  
    -   [Pagina Aggiorna configurazione](#Update_configuration)  
  
    -   [Pagina Riepilogo](#Summary)  
  
    -   [Pagina Distribuisci](#Deploy)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per la distribuzione di un'applicazione livello dati.  
  
 **Non visualizzare più questa pagina** - Fare clic sulla casella di controllo per evitare che la pagina venga visualizzata nuovamente in futuro.  
  
 **Avanti >**: consente di passare alla pagina **Selezione pacchetto di applicazione livello dati**.  
  
 **Annulla** consente di terminare la procedura guidata senza distribuire un'applicazione livello dati.  
  
##  <a name="select-dac-package-page"></a><a name="Select_dac_package"></a>Pagina Seleziona pacchetto di applicazione livello dati  
 Usare questa pagina per specificare il pacchetto di applicazione livello dati contenente l'applicazione livello dati da distribuire. La pagina passa attraverso tre stati.  
  
### <a name="select-the-dac-package"></a>Selezionare pacchetto di applicazione livello dati  
 Usare lo stato iniziale della pagina per scegliere il pacchetto di applicazione livello dati da distribuire. È necessario specificare un file di pacchetto di applicazione livello dati valido con estensione dacpac.  
  
 **Pacchetto di applicazione livello dati** : consente di specificare il percorso e il nome file del pacchetto di applicazione livello dati contenente l'applicazione livello dati da distribuire. Per passare al percorso del pacchetto di applicazione livello dati, è possibile fare clic sul pulsante **Sfoglia** a destra della casella.  
  
 **Nome applicazione** casella di sola lettura in cui viene visualizzato il nome dell'applicazione livello dati assegnato durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Versione** casella di sola lettura in cui viene visualizzata la versione assegnata durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Descrizione**: casella di sola lettura in cui viene visualizzata la descrizione immessa durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 ** \< Indietro** : consente di tornare alla pagina **Introduzione** .  
  
 **Avanti >**: consente di visualizzare un indicatore di stato per la verifica della validità del file selezionato come pacchetto di applicazione livello dati.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
### <a name="validating-the-dac-package"></a>Convalida del pacchetto di applicazione livello dati  
 Viene visualizzato un indicatore di stato per la verifica della validità del file selezionato come pacchetto di applicazione livello dati. Se il pacchetto di applicazione livello dati viene convalidato, la procedura guidata continua con la versione finale della pagina **Seleziona pacchetto** in cui è possibile controllare il risultato della convalida. Se il file non è un pacchetto di applicazione livello dati valido, rimane visualizzata la pagina **Selezione pacchetto di applicazione livello dati**. Selezionare un altro pacchetto di applicazione livello dati valido o annullare la procedura guidata e generare un nuovo pacchetto di applicazione livello dati.  
  
 **Convalida del contenuto dell'applicazione livello dati**: indicatore di stato che segnala lo stato corrente del processo di convalida.  
  
 ** \< Indietro** : consente di tornare allo stato iniziale della pagina **Seleziona pacchetto** .  
  
 **Avanti >**: consente di passare alla versione finale della pagina **Seleziona pacchetto**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="review-policy-page"></a><a name="Review_policy"></a> Pagina Verifica criteri  
 Usare questa pagina per controllare il risultato della valutazione degli eventuali criteri di selezione dei server dell'applicazione livello dati. I criteri di selezione dei server del pacchetto di applicazione livello dati sono facoltativi e sono assegnati al pacchetto di applicazione livello dati quando viene creato in Visual Studio. I facet dei criteri di selezione dei server vengono usati per specificare le condizioni che un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve soddisfare per ospitare il pacchetto DAC.  
  
 **Risultati della valutazione delle condizioni dei criteri** report di sola lettura che indica se le condizioni dei criteri di distribuzione dell'applicazione livello dati sono soddisfatte. I risultati della valutazione di ogni condizione sono riportati in una riga distinta.  
  
 I criteri di selezione dei server riportati di seguito vengono valutati sempre come falsi durante la distribuzione di un'applicazione livello dati a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: versione del sistema operativo, lingua, Named Pipes abilitato, piattaforma e tcp abilitato.  
  
 **Ignora le violazioni dei criteri** : usare questa casella di controllo per continuare la distribuzione se una o più delle condizioni dei criteri non sono soddisfatte. Selezionare questa opzione solo se si è sicuri che tutte le condizioni non soddisfatte non impediranno la distribuzione del pacchetto DAC.  
  
 ** \< Indietro** : consente di tornare alla pagina **Seleziona pacchetto** .  
  
 **Avanti >**: consente di passare alla pagina **Aggiorna configurazione**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="update-configuration-page"></a><a name="Update_configuration"></a>Aggiorna pagina di configurazione  
 Usare questa pagina per specificare i nomi dell'istanza di applicazione livello dati distribuita e del database creato dalla distribuzione e per impostare le opzioni del database.  
  
 **Nome database** : consente di specificare il nome del database da creare con la distribuzione. Il nome predefinito corrisponde al nome del database di origine da cui è stato estratto il pacchetto di applicazione livello dati. Il nome deve essere univoco all'interno dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ed essere conforme alle regole per gli identificatori del [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Se si modifica il nome del database, i nomi del file di dati e del file di log verranno modificati in modo da corrispondere al nuovo valore.  
  
 Il nome del database viene inoltre usato come nome dell'istanza di applicazione livello dati. Il nome dell'istanza è visualizzato nel nodo dell'applicazione livello dati, nel nodo **Applicazioni livello dati** in **Esplora oggetti**o nel nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in **Esplora utilità**.  
  
 Le opzioni seguenti non si applicano a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]e non vengono visualizzate in caso di distribuzione in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Usa percorso predefinito file di database** : selezionare questa opzione per creare i file di dati e di log del database nel percorso predefinito per l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. I nomi dei file saranno creati usando il nome del database.  
  
 **Specifica file di database** : selezionare questa opzione per specificare un percorso o un nome diverso per i file di dati e di log.  
  
 **Percorso e nome file di dati** : consente di specificare il percorso completo e il nome del file di dati. La casella viene popolata con il percorso e il nome file predefiniti. Modificare la stringa nella casella per modificare l'impostazione predefinita oppure usare il pulsante Sfoglia per passare alla cartella in cui si desidera salvare il file di dati.  
  
 **Percorso e nome file di log** : consente di specificare il percorso completo e il nome del file di log. La casella viene popolata con il percorso e il nome file predefiniti. Modificare la stringa nella casella per modificare l'impostazione predefinita oppure usare il pulsante **Sfoglia** per passare alla cartella in cui si desidera salvare il file di log.  
  
 ** \< Indietro** : consente di tornare alla pagina **Seleziona pacchetto di applicazione livello dati** .  
  
 **Avanti >**: consente di passare alla pagina **Riepilogo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="summary-page"></a><a name="Summary"></a> Pagina Riepilogo  
 Usare questa pagina per controllare le azioni che verranno eseguite dalla procedura guidata durante la distribuzione del pacchetto di applicazione livello dati.  
  
 **Le impostazioni seguenti saranno usate per implementare l'applicazione livello dati.** Controllare le informazioni visualizzate per assicurarsi che le azioni che verranno eseguite siano corrette. Nella finestra viene visualizzato il pacchetto di applicazione livello dati selezionato e il nome selezionato per l'istanza di applicazione livello dati distribuita. Nella finestra vengono inoltre visualizzate le impostazioni che verranno usate durante la creazione del database associato al pacchetto di applicazione livello dati.  
  
 ** \< Indietro** : consente di tornare alla pagina di **configurazione dell'aggiornamento** per modificare le selezioni effettuate.  
  
 **Avanti >**: consente di distribuire l'applicazione livello dati e visualizzare i risultati nella pagina **Distribuisci DAC**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="deploy-page"></a><a name="Deploy"></a>Pagina Distribuisci  
 In questa pagina viene segnalato l'esito positivo o negativo dell'operazione di distribuzione.  
  
 **Distribuzione dell'applicazione livello dati** : consente di visualizzare l'esito positivo o negativo di ogni azione eseguita per distribuire l'applicazione livello dati. Verificare le informazioni che determinano l'esito positivo o negativo di ciascuna azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Selezionare il collegamento per visualizzare un report dell'errore per l'azione.  
  
 **Salva report** : consente di salvare il report della distribuzione come file HTML. Nel file viene riportato lo stato di ogni azione, inclusi tutti gli errori generati da qualsiasi azione. La cartella predefinita è la cartella SQL Server Management Studio\DAC Packages contenuta nella cartella Documenti dell'account di Windows.  
  
 **Fine** : consente di terminare la procedura guidata.  
  
##  <a name="using-powershell"></a><a name="DeployDACPowerShell"></a> Utilizzo di PowerShell  
 **Per distribuire un'applicazione livello dati usando il metodo Install() in uno script di PowerShell**  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza a cui distribuire l'applicazione livello dati.  
  
2.  Aprire un oggetto `ServerConnection` e collegarlo alla stessa istanza.  
  
3.  Usare `System.IO.File` per caricare il file del pacchetto di applicazione livello dati.  
  
4.  Usare `add_DacActionStarted` e `add_DacActionFinished` per sottoscrivere gli eventi di distribuzione dell'applicazione livello dati.  
  
5.  Impostare `DatabaseDeploymentProperties`.  
  
6.  Usare il metodo `DacStore.Install` per distribuire l'applicazione livello dati.  
  
7.  Chiudere il flusso di file usato per leggere il file del pacchetto di applicazione livello dati.  
  
### <a name="example-powershell"></a>Esempio (PowerShell)  
 Nel seguente esempio viene distribuita un'applicazione livello dati denominata MyApplication su un'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)], usando una definizione dell'applicazione livello dati in un pacchetto MyApplication.dacpac.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](data-tier-applications.md)   
 [Estrarre un'applicazione livello dati da un database](extract-a-dac-from-a-database.md)   
 [Identificatori del database](../databases/database-identifiers.md)  
