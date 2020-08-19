---
description: Eliminazione di un'applicazione livello dati
title: Eliminare un'applicazione livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2bde888ff6091ae8d05445acce1afb1469843c18
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386637"
---
# <a name="delete-a-data-tier-application"></a>Eliminazione di un'applicazione livello dati
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  È possibile eliminare un'applicazione livello dati utilizzando la procedura guidata Elimina applicazione livello dati o uno script Windows PowerShell. È possibile specificare se il database associato viene mantenuto, scollegato o eliminato.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per aggiornare un'applicazione livello dati tramite la:**  [Procedura guidata Elimina applicazione livello dati](#UsingDeleteDACWizard), [PowerShell](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Quando si elimina un'istanza di applicazione livello dati (DAC), è necessario selezionare una tra tre opzioni in cui viene specificata l'azione che verrà eseguita con il database associato all'applicazione livello dati. Tutte e tre le opzioni consentono di eliminare i metadati che definiscono l'applicazione livello dati. Le opzioni differiscono tra loro per le azioni relative al database associato all'applicazione livello dati. Con la procedura guidata non viene eliminato alcun oggetto a livello di istanza associato all'applicazione livello dati o al database, come ad esempio gli account di accesso.  
  
|Opzione|Azioni di database|  
|------------|----------------------|  
|Elimina registrazione|Il database associato rimane intatto.|  
|Scollega database|Il database associato viene scollegato. L'istanza del Motore di database non potrà fare riferimento al database, ma i file di dati e di log rimarranno invariati.|  
|Elimina database|Il database associato viene eliminato. I file di dati e di log vengono eliminati.|  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Non esistono meccanismi automatici per ripristinare i metadati della definizione o il database dell'applicazione livello dati dopo l'eliminazione dell'applicazione. Il metodo per ricompilare manualmente l'istanza di applicazione livello dati dipende dall'opzione di eliminazione scelta.  
  
|Opzione|Metodo di ricompilazione dell'istanza di applicazione livello dati|  
|------------|-------------------------------------|  
|Elimina registrazione|Registrare un'applicazione livello dati dal database rimasto.|  
|Scollega database|Collegare nuovamente il database tramite **sp_attachdb** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi registrare una nuova istanza di applicazione livello dati dal database.|  
|Elimina database|Ripristinare il database da un backup completo eseguito prima dell'eliminazione dell'applicazione livello dati, quindi registrare una nuova istanza di applicazione livello dati dal database.|  
  
> [!WARNING]  
>  La ricompilazione di un'istanza di applicazione livello dati mediante la registrazione di un'applicazione livello dati da un database ripristinato o ricollegato non implica la ricreazione di alcune parti dell'applicazione originale, quali i criteri di selezione dei server.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Un'applicazione livello dati può essere eliminata unicamente da membri del ruolo predefinito del server **sysadmin** o **serveradmin** oppure dal proprietario del database. È inoltre possibile avviare la procedura guidata usando l'account dell'amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito denominato **sa** .  
  
##  <a name="using-the-delete-data-tier-application-wizard"></a><a name="UsingDeleteDACWizard"></a> Utilizzo della procedura guidata Elimina applicazione livello dati  
 **Per eliminare un'applicazione livello dati tramite una procedura guidata**  
  
1.  In **Esplora oggetti**espandere il nodo dell'istanza contenente l'applicazione livello dati da eliminare.  
  
2.  Espandere il nodo **Gestione** .  
  
3.  Espandere il nodo **Applicazioni livello dati** .  
  
4.  Fare clic con il pulsante destro del mouse sull'applicazione livello dati (DAC) da eliminare e quindi selezionare **Elimina applicazione livello dati**.  
  
5.  Completare le finestre di dialogo della procedura guidata.  
  
    1.  [Introduzione](#Introduction)  
  
    2.  [Seleziona metodo](#Choose_method)  
  
    3.  [Summary](#Summary)  
  
    4.  [Elimina applicazione livello dati](#Delete_datatier_application)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> Pagina Introduzione  
 In questa pagina vengono descritti i passaggi per l'eliminazione di un'applicazione livello dati.  
  
 **Non visualizzare più questa pagina** - Fare clic sulla casella di controllo per evitare che la pagina venga visualizzata nuovamente in futuro.  
  
 **Avanti >**: consente di passare alla pagina **Seleziona metodo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza eliminare un'applicazione livello dati o un database.  
  
 [Utilizzo della procedura guidata Elimina applicazione livello dati](#UsingDeleteDACWizard)  
  
##  <a name="choose-method-page"></a><a name="Choose_method"></a> Pagina Seleziona metodo  
 Utilizzare questa pagina per specificare l'opzione per la gestione del database associato all'applicazione livello dati da eliminare.  
  
 **Elimina registrazione** : consente di rimuovere i metadati che definiscono l'applicazione livello dati lasciando intatto il database associato.  
  
 **Scollega database** : consente di rimuovere i metadati che definiscono l'applicazione livello dati e scollegare il database associato.  
  
 L'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]non può più fare riferimento al database, ma i dati e il file di log rimangono intatti.  
  
 **Elimina database** : consente di rimuovere i metadati che definiscono l'applicazione livello dati ed eliminare il database associato.  
  
 I dati e i file di log per il database vengono definitivamente eliminati.  
  
 **< Indietro**: consente di tornare alla pagina **Introduzione**.  
  
 **Avanti >**: consente di passare alla pagina **Riepilogo**.  
  
 **Annulla** : consente di terminare la procedura guidata senza eliminare l'applicazione livello dati o il database.  
  
 [Utilizzo della procedura guidata Elimina applicazione livello dati](#UsingDeleteDACWizard)  
  
##  <a name="summary-page"></a><a name="Summary"></a> Pagina Riepilogo  
 Utilizzare questa pagina per verificare le azioni eseguite dalla procedura guidata in caso di eliminazione dell'istanza di applicazione livello dati.  
  
 **Controlla selezioni** : consente di verificare l'applicazione livello dati, il database e il metodo di eliminazione visualizzato nella casella. Se le informazioni sono corrette, selezionare **Avanti** o **Fine** per eliminare l'applicazione livello dati. Se l'applicazione livello dati e le informazioni del database non sono corrette, selezionare **Annulla** , quindi l'applicazione livello dati corretta. Se il metodo di eliminazione non è corretto, scegliere **Indietro** per tornare alla pagina **Seleziona metodo** e selezionare un altro metodo.  
  
 **< Indietro**: consente di tornare alla pagina **Seleziona metodo** per selezionare un altro metodo di eliminazione.  
  
 **Avanti >**: consente di eliminare l'istanza DAC usando il metodo selezionato nella pagina precedente e passare alla pagina **Elimina applicazione del livello dati**.  
  
 **Annulla** : consente di terminare la procedura guidata senza eliminare l'istanza di applicazione livello dati.  
  
 [Utilizzo della procedura guidata Elimina applicazione livello dati](#UsingDeleteDACWizard)  
  
##  <a name="delete-data-tier-application-page"></a><a name="Delete_datatier_application"></a> Pagina Elimina applicazione livello dati  
 In questa pagina viene indicato l'esito positivo o negativo dell'operazione di eliminazione.  
  
 **Eliminazione dell'applicazione livello dati** : consente di visualizzare l'esito positivo o negativo di ogni azione eseguita per l'eliminazione dell'istanza di applicazione livello dati. Verificare le informazioni che determinano l'esito positivo o negativo di ciascuna azione. Ogni azione che ha rilevato un errore avrà un collegamento nella colonna **Risultato** . Selezionare il collegamento per visualizzare un report dell'errore per l'azione.  
  
 **Salva report** : consente di salvare il report dell'eliminazione come file HTML. Nel file viene riportato lo stato di ogni azione, inclusi tutti gli errori generati da qualsiasi azione. La cartella predefinita è una cartella SQL Server Management Studio\DAC Packages contenuta all'interno della cartella Documenti dell'account di Windows.  
  
 **Fine** : consente di terminare la procedura guidata.  
  
 [Utilizzo della procedura guidata Elimina applicazione livello dati](#UsingDeleteDACWizard)  
  
##  <a name="using-powershell"></a><a name="DeleteDACPowerShell"></a> Utilizzo di PowerShell  

1. Creare un oggetto server SMO e impostarlo sull'istanza contenente l'applicazione livello dati da eliminare.  
  
1. Aprire un oggetto **ServerConnection** e connetterlo alla stessa istanza.  
  
1. Utilizzare `add_DacActionStarted` e `add_DacActionFinished` per sottoscrivere gli eventi dell'aggiornamento dell'applicazione livello dati.  
  
1. Specificare l'applicazione livello dati da eliminare.  
  
1. Usare uno dei tre esempi, in base all'opzione di eliminazione appropriata:  
  
   - Per eliminare la registrazione dell'applicazione livello dati e lasciare intatto il database, usare il metodo `Unmanage`.  
   - Per eliminare la registrazione dell'applicazione livello dati e scollegare il database, utilizzare il metodo `Uninstall` e specificare `DetachDatabase`.  
   - Per eliminare la registrazione dell'applicazione livello dati ed eliminare il database, utilizzare il metodo `Uninstall` e specificare `DropDatabase`.
  
### <a name="delete-the-dac-and-leave-the-database"></a>Eliminare l'applicazione livello dati e lasciare il database

Nell'esempio seguente viene eliminata un'applicazione livello dati denominata `<myApplication>` usando il metodo `Unmanage` per eliminare l'applicazione livello dati lasciando intatto il database.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacStore.Unmanage($dacName)  
```
  
### <a name="delete-the-dac-and-detach-the-database"></a>Eliminare l'applicazione livello dati e scollegare il database

Nell'esempio seguente viene eliminata un'applicazione livello dati denominata `<myApplication>` usando il metodo `Uninstall` per eliminare l'applicazione livello dati e scollegare il database.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacStore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```
  
### <a name="delete-the-dac-and-drop-the-database"></a>Eliminare l'applicazione livello dati ed eliminare il database

Nell'esempio seguente viene eliminata un'applicazione livello dati denominata `<myApplication>` usando il metodo `Uninstall` per eliminare l'applicazione livello dati ed eliminare il database.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$server = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($server.ConnectionContext.SqlConnectionObject)  
$serverConnection.Connect()  
$dacStore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverConnection)  
  
## Subscribe to the DAC delete events.  
$dacStore.add_DacActionStarted({Write-Host `n`nStarting at $(Get-Date) :: $_.Description})  
$dacStore.add_DacActionFinished({Write-Host Completed at $(Get-Date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "<myApplication>"  
  
## Delete the DAC definition from msdb and drop the associated database.  
$dacStore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Distribuire un'applicazione livello dati](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Registrare un database come applicazione livello dati](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
