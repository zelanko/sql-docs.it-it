---
title: Aggiornare un'applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.upgradedacwizard.reviewpolicy.f1
- sql12.swb.upgradedacwizard.selectoptions.f1
- sql12.swb.upgradedacwizard.selectpackage.f1
- sql12.swb.upgradedacwizard.reviewplan.f1
- sql12.swb.upgradedacwizard.checkdrift.f1
- sql12.swb.upgradedacwizard.summary.f1
- sql12.swb.upgradedacwizard.upgradedac.f1
- sql12.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 44c4bb7c01f18db6062ad1982fcf5a5f80e4d6b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797982"
---
# <a name="upgrade-a-data-tier-application"></a>Upgrade a Data-tier Application
  Utilizzare la procedura guidata Aggiorna applicazione livello dati o uno script di Windows PowerShell per modificare lo schema e le proprietà di un'applicazione livello dati (DAC) attualmente distribuita affinché corrispondano allo schema e alle proprietà definite in una nuova versione dell'applicazione livello dati.  
  
-   **Prima di iniziare:**  [Scelta delle opzioni di aggiornamento dell'applicazione livello dati](#ChoseDACUpgOptions), [Limitazioni e restrizioni](#LimitationsRestrictions), [Prerequisiti](#Prerequisites), [Sicurezza](#Security), [Autorizzazioni](#Permissions)  
  
-   **Per aggiornare un'applicazione livello dati tramite la:**  [Procedura guidata Aggiorna applicazione livello dati](#UsingDACUpgradeWizard), [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Un aggiornamento dell'applicazione livello dati è un processo sul posto che consente di modificare lo schema del database esistente affinché corrisponda allo schema definito in una nuova versione dell'applicazione livello dati. La nuova versione dell'applicazione livello dati è fornita in un file del pacchetto di applicazione livello dati. Per altre informazioni sulla creazione di un pacchetto di applicazione livello dati, vedere [Applicazioni livello dati](data-tier-applications.md).  
  
###  <a name="choosing-dac-upgrade-options"></a><a name="ChoseDACUpgOptions"></a> Scelta delle opzioni di aggiornamento dell'applicazione livello dati  
 Sono disponibili quattro opzioni per un aggiornamento sul posto:  
  
-   **Ignora perdita di dati** - `True`se, l'aggiornamento continuerà anche se alcune delle operazioni comportano la perdita di dati. Se `False`, queste operazioni comporteranno l'interruzione dell'aggiornamento. Ad esempio, se una tabella nel database corrente non è presente nello schema della nuova applicazione livello dati, la tabella viene eliminata se è specificato `True`. L'impostazione predefinita è `True`.  
  
-   **Blocca in** caso di modifiche `True`: se, l'aggiornamento viene terminato se lo schema del database è diverso da quello definito nell'applicazione livello dati precedente. Se `False`, l'aggiornamento continua anche se vengono rilevate delle modifiche. L'impostazione predefinita è `False`.  
  
-   **Rollback in caso di errore** : se `True`, l'aggiornamento è incluso in una transazione e se si verificano errori, verrà effettuato un tentativo di rollback. Se `False`, viene eseguito il commit di tutte le modifiche nel momento in cui vengono apportate e, in caso di errori, potrebbe essere necessario ripristinare un backup precedente del database. L'impostazione predefinita è `False`.  
  
-   **Ignora convalida criteri** -se `True`, i criteri di selezione del server DAC non vengono valutati. Se `False`, vengono valutati i criteri e l'aggiornamento termina in caso di errore di convalida. L'impostazione predefinita è `False`.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 È possibile eseguire aggiornamenti dell'applicazione livello dati solo in [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o versioni successive.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 È consigliabile eseguire un backup completo del database prima di avviare l'aggiornamento. Se durante un aggiornamento viene rilevato un errore e non è possibile eseguire il rollback di tutte le relative modifiche, potrebbe essere necessario ripristinare il backup.  
  
 Prima di dare inizio all'aggiornamento, è necessario intraprendere diverse azioni per la convalida del pacchetto di applicazione livello dati e delle azioni di aggiornamento. Per altre informazioni su come eseguire questi controlli, vedere [Validate a DAC Package](validate-a-dac-package.md).  
  
-   È consigliabile evitare di eseguire l'aggiornamento tramite pacchetti di applicazioni livello dati provenienti da origini sconosciute o non attendibili. Tali pacchetti possono contenere codice dannoso che potrebbe eseguire codice indesiderato Transact-SQL o causare errori modificando lo schema. Prima di usare un pacchetto proveniente da un'origine sconosciuta o non attendibile, decomprimerlo e controllare il codice, ad esempio le stored procedure o altro codice definito dall'utente.  
  
-   Se sono state apportate modifiche al database corrente dopo che è stata distribuita l'ultima versione dell'applicazione livello dati, alcune delle modifiche potrebbero impedire il completamento dell'aggiornamento o essere rimosse in seguito all'aggiornamento. È necessario innanzitutto generare ed esaminare un report per analizzare modifiche di questo tipo apportate al database.  
  
-   È consigliabile generare un elenco delle modifiche dello schema che verranno eseguite dall'aggiornamento e controllare l'elenco per rilevare eventuali problemi.  
  
 Il nome dell'applicazione nel pacchetto di applicazione livello dati deve corrispondere al nome dell'applicazione livello dati attualmente distribuita. Se ad esempio il nome dell'applicazione livello dati è **GeneralLedger**, è possibile eseguire l'aggiornamento solo tramite un pacchetto di applicazione livello dati il cui nome di applicazione sia **GeneralLedger**.  
  
 Assicurarsi che ci sia abbastanza spazio del log delle transazioni disponibile per registrare tutte le modifiche.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per migliorare la sicurezza, gli account di accesso dell'autenticazione di SQL Server vengono archiviati in un pacchetto di applicazione livello dati senza password. Quando il pacchetto viene distribuito o aggiornato, l'account di accesso viene creato come account disabilitato con una password generata. Per abilitare gli account di accesso, è necessario accedere usando un account che dispone dell'autorizzazione ALTER ANY LOGIN e usare ALTER LOGIN per abilitare l'account di accesso e assegnare una nuova password che può essere comunicata all'utente. Questa operazione non è necessaria per gli account di accesso dell'autenticazione di Windows, in quanto le relative password non sono gestite da SQL Server.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Un'applicazione livello dati può essere aggiornata unicamente da membri del ruolo predefinito del server **sysadmin** o **serveradmin** oppure tramite account di accesso nel ruolo predefinito del server **dbcreator** con autorizzazioni ALTER ANY LOGIN. È necessario che l'accesso venga eseguito come proprietario del database esistente. È anche possibile aggiornare un'applicazione livello dati con l'account amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito denominato **sa** .  
  
##  <a name="using-the-upgrade-data-tier-application-wizard"></a><a name="UsingDACUpgradeWizard"></a> Utilizzo della procedura guidata Aggiorna applicazione di livello dati  
 **Per aggiornare un'applicazione livello dati tramite una procedura guidata**  
  
1.  In **Esplora oggetti**espandere il nodo dell'istanza contenente l'applicazione livello dati da aggiornare.  
  
2.  Espandere il nodo **Gestione** , quindi espandere il nodo **Applicazioni livello dati** .  
  
3.  Fare clic con il pulsante destro del mouse sul nodo dell'applicazione livello dati da aggiornare e quindi scegliere **Aggiorna applicazione livello dati**.  
  
4.  Completare le finestre di dialogo della procedura guidata.  
  
    1.  [Pagina Introduzione](#Introduction)  
  
    2.  [Pagina Seleziona pacchetto](#Select_dac_package)  
  
    3.  [Pagina Verifica criteri](#Review_policy)  
  
    4.  [Pagina Rileva modifiche](#Detect_change)  
  
    5.  [Controllare il piano di aggiornamento](#ReviewUpgPlan)  
  
    6.  [Pagina Riepilogo](#Summary)  
  
    7.  [Pagina Aggiorna applicazione livello dati](#Upgrade)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per l'aggiornamento di un'applicazione livello dati.  
  
 **Non visualizzare più questa pagina** - Fare clic sulla casella di controllo per evitare che la pagina venga visualizzata nuovamente in futuro.  
  
 **Avanti >** : consente di passare alla pagina **Seleziona pacchetto**.  
  
 **Annulla** : consente di terminare la procedura guidata senza aggiornare l'applicazione livello dati.  
  
##  <a name="select-package-page"></a><a name="Select_dac_package"></a> Pagina Seleziona pacchetto  
 Utilizzare questa pagina per specificare il pacchetto di applicazione livello dati contenente la nuova versione dell'applicazione livello dati. La pagina passa attraverso due stati.  
  
### <a name="select-the-dac-package"></a>Selezionare pacchetto di applicazione livello dati  
 Usare lo stato iniziale della pagina per scegliere il pacchetto di applicazione livello dati da distribuire. È necessario specificare un file di pacchetto di applicazione livello dati valido con estensione dacpac. Il nome dell'applicazione nel pacchetto di applicazione livello dati deve corrispondere al nome dell'applicazione del pacchetto di applicazione livello dati corrente.  
  
 **Pacchetto di applicazione livello dati** : consente di specificare il percorso e il nome file del pacchetto di applicazione livello dati contenente la nuova versione dell'applicazione livello dati. Per passare al percorso del pacchetto di applicazione livello dati, è possibile fare clic sul pulsante **Sfoglia** a destra della casella.  
  
 **Nome applicazione** casella di sola lettura in cui viene visualizzato il nome dell'applicazione livello dati assegnato durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Versione** casella di sola lettura in cui viene visualizzata la versione assegnata durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 **Descrizione**: casella di sola lettura in cui viene visualizzata la descrizione immessa durante la creazione o l'estrazione dell'applicazione livello dati da un database.  
  
 Indietro: consente di tornare alla pagina **Introduzione** . ** \< **  
  
 **Avanti >** : consente di visualizzare un indicatore di stato per la verifica della validità del file selezionato come pacchetto di applicazione livello dati.  
  
 **Annulla** : consente di terminare la procedura guidata senza aggiornare l'applicazione livello dati.  
  
### <a name="validating-the-dac-package"></a>Convalida del pacchetto di applicazione livello dati  
 Viene visualizzato un indicatore di stato per la verifica della validità del file selezionato come pacchetto di applicazione livello dati. Se il pacchetto di applicazione livello dati viene convalidato, la procedura guidata continua con la pagina **Verifica criteri** . Se il file non è un pacchetto di applicazione livello dati valido, rimane visualizzata la pagina **Selezione pacchetto di applicazione livello dati** . Selezionare un altro pacchetto di applicazione livello dati valido o annullare la procedura guidata e generare un nuovo pacchetto di applicazione livello dati.  
  
 **Convalida del contenuto dell'applicazione livello dati**: indicatore di stato che segnala lo stato corrente del processo di convalida.  
  
 Indietro: consente di tornare allo stato iniziale della pagina **Seleziona pacchetto** . ** \< **  
  
 **Avanti >** : consente di passare alla versione finale della pagina **Seleziona pacchetto**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="review-policy-page"></a><a name="Review_policy"></a> Pagina Verifica criteri  
 Usare questa pagina per controllare il risultato della valutazione degli eventuali criteri di selezione dei server dell'applicazione livello dati. I criteri di selezione dei server del pacchetto DAC sono facoltativi e sono assegnati a un pacchetto DAC creato in Microsoft Visual Studio. I facet dei criteri di selezione dei server vengono usati per specificare le condizioni che un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve soddisfare per ospitare il pacchetto DAC.  
  
 **Risultati della valutazione delle condizioni dei criteri** : report di sola lettura che indica se le valutazioni delle condizioni dei criteri di selezione del server di applicazione livello dati sono soddisfatte. I risultati della valutazione di ogni condizione sono riportati in una riga distinta.  
  
 **Ignora le violazioni dei criteri** : usare questa casella di controllo per continuare l'aggiornamento se una o più delle condizioni dei criteri non sono soddisfatte. Selezionare questa opzione solo se si è sicuri che tutte le condizioni non soddisfatte non impediranno la distribuzione del pacchetto DAC.  
  
 Indietro: consente di tornare alla pagina **Seleziona pacchetto** . ** \< **  
  
 **Avanti >** : consente di passare alla pagina **Rileva modifiche**.  
  
 **Annulla** : consente di terminare la procedura guidata senza aggiornare l'applicazione livello dati.  
  
##  <a name="detect-change-page"></a><a name="Detect_change"></a> Pagina Rileva modifiche  
 In questa pagina vengono visualizzati i risultati dei controlli effettuati dalla procedura guidata sulle modifiche apportate al database che rendono lo schema diverso rispetto alla relativa definizione archiviata nei metadati dell'applicazione livello dati di **msdb**. Viene segnalato ad esempio se sono state utilizzate istruzioni CREATE, ALTER o DROP per aggiungere, modificare o rimuovere oggetti dal database dopo la distribuzione originale dell'applicazione livello dati. Nella pagina viene dapprima visualizzato un indicatore di stato, quindi vengono visualizzati i risultati dell'analisi.  
  
 **Rilevamento delle modifiche in corso. L'operazione potrebbe richiedere alcuni minuti** : viene visualizzato un indicatore di stato che indica il rilevamento delle differenze tra lo schema corrente del database e gli oggetti nella definizione di applicazione livello dati.  
  
 **Risultati rilevamento modifiche** : indica che l'analisi è stata completata e ne visualizza i risultati.  
  
 **Il database NomeDatabase non è stato modificato** : indica che la procedura guidata non ha rilevato differenze tra gli oggetti definiti nel database e le relative controparti nella definizione di applicazione livello dati.  
  
 **Il database NomeDatabase è stato modificato** indica che la procedura guidata ha rilevato modifiche tra gli oggetti definiti nel database e le relative controparti nella definizione di applicazione livello dati.  
  
 **Continua ignorando la possibile perdita delle modifiche** specifica che l'utente è consapevole che alcuni degli oggetti o dei dati nel database corrente non saranno presenti nel nuovo database e che vuole procedere con l'aggiornamento. Scegliere questo pulsante solo se il report delle modifiche è stato analizzato e si conoscono i passaggi che è necessario eseguire per trasferire manualmente oggetti o dati necessari nel nuovo database. In caso di dubbi, fare clic sul pulsante **Salva report** per salvare il report delle modifiche, quindi fare clic su **Annulla**. Analizzare il report, pianificare come trasferire gli oggetti e i dati necessari al termine dell'aggiornamento, quindi riavviare la procedura guidata.  
  
 **Salva report** : fare clic su questo pulsante per salvare un report delle modifiche rilevate dalla procedura guidata tra gli oggetti nel database e le relative controparti nella definizione di applicazione livello dati. È quindi possibile controllare il report per determinare se è necessario eseguire altre operazioni al termine dell'aggiornamento per incorporare alcuni o tutti gli oggetti elencati nel report nel nuovo database.  
  
 Indietro: consente di tornare alla pagina **Seleziona pacchetto di applicazione livello dati** . ** \< **  
  
 **Avanti >** : consente di passare alla pagina **Opzioni**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
## <a name="options-page"></a>Pagina Opzioni  
 Utilizzare questa pagina per selezionare l'opzione Rollback in caso di errore per l'aggiornamento.  
  
 **Rollback in caso di errore**: selezionare questa opzione per includere l'aggiornamento in una transazione su cui la procedura guidata può provare a eseguire il rollback se si verificano errori. Per ulteriori informazioni sull'opzione, vedere [Scelta delle opzioni di aggiornamento dell'applicazione livello dati](#ChoseDACUpgOptions).  
  
 **Ripristina impostazioni predefinite**: consente di ripristinare l'impostazione predefinita dell'opzione, ovvero False.  
  
 Indietro: consente di tornare alla pagina **rileva modifiche** . ** \< **  
  
 **Avanti >** : consente di passare alla pagina **Revisione del piano di aggiornamento**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="review-the-upgrade-plan-page"></a><a name="ReviewUpgPlan"></a> Pagina Revisione del piano di aggiornamento  
 Utilizzare questa pagina per controllare le azioni che verranno eseguite tramite il processo di aggiornamento. Continuare solo se si è sicuri che l'aggiornamento non crei problemi.  
  
 **Le azioni seguenti saranno utilizzate per aggiornare l'applicazione livello dati.** Controllare le informazioni visualizzate per assicurarsi che le azioni che verranno eseguite siano corrette. Nella colonna **Azione** sono visualizzate le azioni, ad esempio le istruzioni Transact-SQL, che verranno eseguite per eseguire l'aggiornamento. Nella colonna **Perdita di dati** sarà contenuto un avviso qualora l'azione associata possa comportare l'eliminazione di dati.  
  
 **Aggiorna**: consente di aggiornare l'elenco di azioni.  
  
 **Salva report azioni**: consente di salvare il contenuto della finestra delle azioni in un file HTML.  
  
 **Continua ignorando la possibile perdita delle modifiche** specifica che l'utente è consapevole che alcuni degli oggetti o dei dati nel database corrente non saranno presenti nel nuovo database e che vuole procedere con l'aggiornamento. Scegliere questo pulsante solo se il report delle modifiche è stato analizzato e si conoscono i passaggi che è necessario eseguire per trasferire manualmente oggetti o dati necessari nel nuovo database. In caso di dubbi, fare clic sul pulsante **Salva report azioni** per salvare il report delle modifiche e sul pulsante **Salva script** per salvare lo script Transact-SQL, quindi scegliere **Annulla**. Analizzare il report e lo script, pianificare come trasferire gli oggetti e i dati necessari al termine dell'aggiornamento, quindi riavviare la procedura guidata.  
  
 **Salva script**: salva in un file di testo le istruzioni Transact-SQL che verranno usate per eseguire l'aggiornamento.  
  
 **Ripristina impostazioni predefinite**: consente di ripristinare l'impostazione predefinita dell'opzione, ovvero False.  
  
 Indietro: consente di tornare alla pagina **rileva modifiche** . ** \< **  
  
 **Avanti >** : consente di passare alla pagina **Riepilogo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="summary-page"></a><a name="Summary"></a> Pagina Riepilogo  
 Utilizzare questa pagina per effettuare una verifica finale delle azioni eseguite dalla procedura guidata durante l'aggiornamento dell'applicazione livello dati.  
  
 **Per aggiornare l'applicazione livello dati saranno utilizzate le seguenti impostazioni.** Controllare le informazioni visualizzate per assicurarsi che le azioni che verranno eseguite siano corrette. Nella finestra viene visualizzata l'applicazione livello dati selezionata per l'aggiornamento e il pacchetto di applicazione livello dati che contiene la nuova versione dell'applicazione. Viene inoltre indicato se la versione corrente del database corrisponde alla definizione dell'applicazione livello dati corrente o se il database è stato modificato.  
  
 Indietro: consente di tornare alla pagina **revisione del piano di aggiornamento** . ** \< **  
  
 **Avanti >** : consente di distribuire l'applicazione livello dati e visualizzare i risultati nella pagina **Aggiorna applicazione livello dati**.  
  
 **Annulla** : consente di terminare la procedura guidata senza distribuire l'applicazione livello dati.  
  
##  <a name="upgrade-dac-page"></a><a name="Upgrade"></a> Pagina Aggiorna applicazione livello dati  
 In questa pagina viene riportato l'esito positivo o negativo dell'operazione di aggiornamento.  
  
 **Aggiornamento del pacchetto DAC** : consente di visualizzare l'esito positivo o negativo di ogni azione eseguita per l'aggiornamento dell'applicazione livello dati. Verificare le informazioni che determinano l'esito positivo o negativo di ciascuna azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Selezionare il collegamento per visualizzare un report dell'errore per l'azione.  
  
 **Salva report** : consente di salvare il report dell'aggiornamento come file HTML. Nel file viene riportato lo stato di ogni azione, inclusi tutti gli errori generati da qualsiasi azione. La cartella predefinita è una cartella SQL Server Management Studio\DAC Packages contenuta all'interno della cartella Documenti dell'account di Windows.  
  
 **Fine** : consente di terminare la procedura guidata.  
  
##  <a name="using-powershell"></a><a name="UpgradeDACPowerShell"></a> Utilizzo di PowerShell  
 **Per aggiornare un'applicazione livello dati usando il metodo IncrementalUpgrade() in uno script di PowerShell**  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza contenente l'applicazione livello dati da aggiornare.  
  
2.  Aprire un oggetto `ServerConnection` e collegarlo alla stessa istanza.  
  
3.  Usare `System.IO.File` per caricare il file del pacchetto di applicazione livello dati.  
  
4.  Utilizzare `add_DacActionStarted` e `add_DacActionFinished` per sottoscrivere gli eventi dell'aggiornamento dell'applicazione livello dati.  
  
5.  Impostare `DacUpgradeOptions`.  
  
6.  Utilizzare il metodo `IncrementalUpgrade` per aggiornare l'applicazione livello dati.  
  
7.  Chiudere il flusso di file usato per leggere il file del pacchetto di applicazione livello dati.  
  
### <a name="example-powershell"></a>Esempio (PowerShell)  
 Nel seguente esempio viene aggiornata un'applicazione livello dati denominata MyApplication su un'istanza predefinita del [!INCLUDE[ssDE](../../includes/ssde-md.md)], utilizzando una nuova versione di applicazione livello dati in un pacchetto MyApplicationVNext.dacpac.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplicationVNext.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](data-tier-applications.md)   
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
