---
title: Convalidare un pacchetto di applicazioni livello dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7df5bb3b2ef677e597d12dad8b8d92ddbb22fcba
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908251"
---
# <a name="validate-a-dac-package"></a>Convalida di un pacchetto di applicazioni livello dati
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È consigliabile esaminare il contenuto di un pacchetto di un'applicazione livello dati prima di distribuirlo nella produzione nonché convalidare le azioni di aggiornamento prima di aggiornare un'applicazione livello dati esistente, in particolare nel caso in cui si distribuiscano pacchetti non sviluppati dalla propria organizzazione.  
  
1.  **Prima di iniziare:**  [Prerequisiti](#Prerequisites)  
  
2.  **Per aggiornare un'applicazione livello dati:**  [Visualizzare il contenuto di un'applicazione livello dati](#ViewDACContents), [Visualizzare modifiche al database](#ViewDBChanges), [Visualizzare azioni di aggiornamento](#ViewUpgradeActions), [Confrontare le applicazioni livello dati](#CompareDACs)  

##  <a name="Prerequisites"></a> Prerequisiti  
 È consigliabile evitare di distribuire un pacchetto di applicazione livello dati proveniente da origini sconosciute o non attendibili. Tali pacchetti DAC possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema. Prima di usare un'applicazione livello dati proveniente da un'origine sconosciuta o non attendibile, distribuirla in un'istanza di test isolata del [!INCLUDE[ssDE](../../includes/ssde-md.md)], eseguire [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) sul database ed esaminare anche il codice nel database, ad esempio stored procedure o altro codice definito dall'utente.  
  
##  <a name="ViewDACContents"></a> Visualizza il contenuto di un'applicazione livello dati  
 Sono disponibili due meccanismi per la visualizzazione del contenuto di un pacchetto di applicazione livello dati (DAC). È possibile importare il pacchetto di applicazione livello dati in un progetto di applicazione livello dati in SQL Server Developer Tools. In alternativa, è possibile decomprimere il contenuto del pacchetto in una cartella.  
  
 **Visualizzare un'applicazione livello dati in SQL Server Developer Tools**  
  
1.  Aprire il menu **File**, selezionare **Nuovo** e quindi **Progetto**.  
  
2.  Selezionare il modello di progetto di **SQL Server** e specificare un **Nome**, una **Percorso**e un **Nome soluzione**.  
  
3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Proprietà**.  
  
4.  Nella scheda **Impostazioni progetto** selezionare la casella di controllo **Applicazione livello dati (file .dacpac)** nella sezione **Tipi di output** e quindi chiudere la finestra di dialogo delle proprietà.  
  
5.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Importa applicazione livello dati**.  
  
6.  Usare **Esplora soluzioni** per aprire tutti i file dell'applicazione livello dati, ad esempio i criteri di selezione dei server e gli script pre-distribuzione e post-distribuzione.  
  
7.  Utilizzare **Visualizzazione schema** per controllare tutti gli oggetti nello schema, rivedendo in particolare il codice di oggetti quali funzioni o stored procedure.  
  
 **Visualizzare un'applicazione livello dati in una cartella**  
  
-   decomprimere il pacchetto di applicazione livello dati in una cartella seguendo le istruzioni riportate in [Unpack a DAC Package](../../relational-databases/data-tier-applications/unpack-a-dac-package.md).  
  
-   Visualizzare il contenuto degli script [!INCLUDE[tsql](../../includes/tsql-md.md)] aprendoli nell'Editor di query [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
-   Visualizzare il contenuto dei file di testo negli strumenti quale Blocco note.  
  
##  <a name="ViewDBChanges"></a> Visualizza modifiche al database  
 Dopo che la versione corrente di un'applicazione livello dati è distribuita a produzione, è possibile che le modifiche siano state apportate direttamente al database associato che potrebbe creare conflitti con lo schema definito in una nuova versione dell'applicazione livello dati. Prima di aggiornare a una nuova versione dell'applicazione livello dati, controllare per vedere se tali modifiche sono state apportate al database.  
  
 **Visualizzare modifiche al Database tramite una procedura guidata**  
  
1.  Eseguire la procedura guidata **Aggiorna applicazione livello dati** , specificare l'applicazione livello dati attualmente distribuita e il pacchetto di applicazione livello dati contenente la nuova versione dell'applicazione stessa.  
  
2.  Nella pagina **Rileva modifiche** , esaminare il report delle modifiche apportate al database.  
  
3.  Selezionare **Annulla** se non si desidera proseguire con l'aggiornamento.  
  
4.  Per altre informazioni sull'uso della procedura guidata, vedere [Aggiornare un'applicazione livello dati](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Visualizzare modifiche al database tramite PowerShell**  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza contenente l'applicazione livello dati da visualizzare.  
  
2.  Aprire un oggetto **ServerConnection** e connetterlo alla stessa istanza.  
  
3.  Specificare il nome dell'applicazione livello dati in una variabile.  
  
4.  Usare il metodo **GetDatabaseChanges()** per recuperare un oggetto **ChangeResults** e inoltrare tramite pipe l'oggetto a un file di testo per generare un report semplice degli oggetti nuovi, eliminati e modificati.  
  
### <a name="view-database-changes-example-powershell"></a>Visualizzare esempio di modifiche al database (PowerShell)  
 **Visualizzare esempio di modifiche al database (PowerShell)**  
  
 Nell'esempio seguente vengono segnalate eventuali modifiche apportate al database in un'applicazione livello dati distribuita denominata MyApplicaiton.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> Visualizza azioni di aggiornamento  
 Prima di utilizzare una nuova versione di un pacchetto di applicazione livello dati per aggiornare un'applicazione livello dati distribuita da un pacchetto di applicazione livello dati precedente, è possibile generare un report in cui sono contenute le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che verranno eseguite durante l'aggiornamento, quindi controllare le istruzioni.  
  
 **Segnalare azioni di aggiornamento tramite una procedura guidata**  
  
1.  Eseguire la procedura guidata **Aggiorna applicazione livello dati** , specificare l'applicazione livello dati attualmente distribuita e il pacchetto di applicazione livello dati contenente la nuova versione dell'applicazione stessa.  
  
2.  Nella pagina **Riepilogo** , esaminare il report delle azioni di aggiornamento.  
  
3.  Selezionare **Annulla** se non si desidera proseguire con l'aggiornamento.  
  
4.  Per altre informazioni sull'uso della procedura guidata, vedere [Aggiornare un'applicazione livello dati](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md).  
  
 **Segnalare azioni di aggiornamento tramite PowerShell**  
  
1.  Creare un oggetto server SMO e impostarlo sull'istanza contenente l'applicazione livello dati distribuita.  
  
2.  Aprire un oggetto **ServerConnection** e connetterlo alla stessa istanza.  
  
3.  Usare **System.IO.File** per caricare il file del pacchetto di applicazione livello dati.  
  
4.  Specificare il nome dell'applicazione livello dati in una variabile.  
  
5.  Usare il metodo **GetIncrementalUpgradeScript()** per ottenere un elenco delle istruzioni Transact-SQL che verrebbero eseguite durante un aggiornamento e inoltrare tramite pipe l'elenco a un file di testo.  
  
6.  Chiudere il flusso di file usato per leggere il file del pacchetto di applicazione livello dati.  
  
### <a name="view-upgrade-actions-example-powershell"></a>Visualizzare esempio di azioni di aggiornamento (PowerShell)  
 **Visualizzare esempio di azioni di aggiornamento (PowerShell)**  
  
 L'esempio seguente illustra le istruzioni Transact-SQL da eseguire per aggiornare un'applicazione livello dati denominata MyApplication allo schema definito in un file MyApplication2017.dacpac.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 Prima di aggiornare un'applicazione del livello dati, è consigliabile controllare le differenze nel database e negli oggetti a livello di istanza tra il pacchetto di applicazioni livello dati corrente e quello nuovo. Se non si dispone di una copia del pacchetto di applicazione livello dati corrente, è possibile estrarre un pacchetto dal database corrente.  
  
 Se si importano entrambi i pacchetti di applicazione livello dati nei progetti di applicazione livello dati in SQL Server Developer Tools, è possibile utilizzare lo strumento di Confronto schema per analizzare le differenze tra i due pacchetti di applicazioni livello dati.  
  
 In alternativa, decomprimere le applicazioni livello dati in cartelle separate. È possibile quindi utilizzare uno strumento delle differenze, quale l'utilità WinDiff, per analizzare le differenze.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Distribuire un'applicazione livello dati](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Aggiornare un'applicazione livello dati](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
