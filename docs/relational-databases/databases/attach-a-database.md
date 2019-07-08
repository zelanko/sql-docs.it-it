---
title: Collegare un database | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3c7b7588801419f57d04996d6bd2cad335a9eede
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583226"
---
# <a name="attach-a-database"></a>Collegare un database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento si illustra come collegare un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. È possibile usare questa funzionalità per copiare, spostare o aggiornare un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="Prerequisites"></a> Prerequisiti  
  
-   Il database deve essere innanzitutto scollegato. Se si tenta di collegare un database che non è stato scollegato, verrà restituito un errore. Per altre informazioni, vedere [Scollegare un database](../../relational-databases/databases/detach-a-database.md).  
  
-   Durante il collegamento di un database è necessario che siano disponibili tutti i file di dati (file MDF e LDF). Se un file di dati si trova in un percorso diverso rispetto al momento della creazione o dell'ultimo collegamento del database, è necessario specificare il percorso corrente.  
  
-   Quando si collega un database, se i file MDF e LDF si trovano in directory diverse e uno dei percorsi include \\\\?\GlobalRoot, l'operazione avrà esito negativo.  
  
###  <a name="Recommendations"></a> Il collegamento è la scelta migliore?  
Quando si spostano file di database all'interno della stessa istanza, è consigliabile spostare i database usando la procedura di rilocazione pianificata `ALTER DATABASE` invece delle operazioni di scollegamento e collegamento. Per altre informazioni, vedere [Spostare database utente](../../relational-databases/databases/move-user-databases.md). 
 
Non è consigliabile usare le operazioni di collegamento e scollegamento da Backup e ripristino. Non esistono backup del log delle transazioni ed è possibile che i file vengano eliminati accidentalmente.
  
###  <a name="Security"></a> Sicurezza  
Le autorizzazioni di accesso ai file vengono impostate durante l'esecuzione di alcune operazioni del database, inclusi il collegamento e lo scollegamento. Per informazioni sulle autorizzazioni per i file impostate quando un database viene collegato o scollegato, vedere [Protezione dei dati e dei file di log](https://technet.microsoft.com/library/ms189128.aspx) dalla [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] documentazione online (lettura ancora valida). 
  
È consigliabile evitare di collegare o ripristinare database provenienti da origini sconosciute o non attendibili. Tali database possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di utilizzare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) sul database in un server non di produzione ed esaminare il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente. Per altre informazioni sul collegamento di database e sulle modifiche apportate ai metadati in caso di collegamento di un database, vedere [Collegamento e scollegamento di un database (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
####  <a name="Permissions"></a> Autorizzazioni  
È necessaria l'autorizzazione `CREATE DATABASE`, `CREATE ANY DATABASE` o `ALTER ANY DATABASE`.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  

### <a name="to-attach-a-database"></a>Per collegare un database  
  
1.  In Esplora oggetti [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ed espandere la vista di questa istanza in SSMS.  
  
2.  Fare clic con il pulsante destro del mouse su **Database** , quindi scegliere **Collega**.  
  
3.  Nella finestra di dialogo **Collega database** fare clic su **Aggiungi**per specificare il database da collegare, quindi nella finestra di dialogo **Individua file di database** selezionare l'unità disco in cui si trova il database ed espandere l'albero di directory per individuare e selezionare il file con estensione mdf del database, ad esempio:  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    > Trying to select a database that is already attached generates an error.  
  
     **Databases to attach**  
     Displays information about the selected databases.  
  
     \<no column header>  
     Displays an icon indicating the status of the attach operation. The possible icons are described in the **Status** description, below).  
  
     **MDF File Location**  
     Displays the path and file name of the selected MDF file.  
  
     **Database Name**  
     Displays the name of the database.  
  
     **Attach As**  
     Optionally, specifies a different name for the database to attach as.  
  
     **Owner**  
     Provides a drop-down list of possible database owners from which you can optionally select a different owner.  
  
     **Status**  
     Displays the status of the database according to the following table.  
  
    |Icona|Testo Stato|Descrizione|  
    |----------|-----------------|-----------------|  
    |(Nessuna icona)|(Nessun testo)|L'operazione di collegamento non è stata avviata o può essere sospesa per questo oggetto. È il valore predefinito all'apertura della finestra di dialogo.|  
    |Triangolo verde che punta a destra|In corso|L'operazione di collegamento è stata avviata ma non ancora completata.|  
    |Segno di spunta verde|Esito positivo|L'oggetto è stato collegato.|  
    |Cerchio rosso con croce bianca|Errore|Si è verificato un errore durante l'operazione. Il collegamento non è stato completato.|  
    |Cerchio con due quadranti neri a destra e a sinistra e due quadranti bianchi in alto e in basso|Stopped|L'operazione di collegamento non è stata completata perché l'utente ne ha arrestato l'esecuzione.|  
    |Cerchio con freccia curva che punta in senso antiorario.|È stato eseguito il rollback|L'operazione di collegamento è stata completata ma ne è stato eseguito il rollback a causa di un errore durante il collegamento di un altro oggetto.|  
  
     **Message**  
     Displays either a blank message or a "File not found" hyperlink.  
  
     **Add**  
     Find the necessary main database files. When the user selects an .mdf file, applicable information is automatically filled in the respective fields of the **Databases to attach** grid.  
  
     **Remove**  
     Removes the selected file from the **Databases to attach** grid.  
  
     **"** *<database_name>* **" database details**  
     Displays the names of the files to be attached. To verify or change the pathname of a file, click the **Browse** button (**...**).  
  
    > [!NOTE]  
    > If a file does not exist, the **Message** column displays "Not found." If a log file is not found, it exists in another directory or has been deleted. You need to either update the file path in the **database details** grid to point to the correct location or remove the log file from the grid. If an .ndf data file is not found, you need to update its path in the grid to point to the correct location.  
  
     **Original File Name**  
     Displays the name of the attached file belonging to the database.  
  
     **File Type**  
     Indicates the type of file, **Data** or **Log**.  
  
     **Current File Path**  
     Displays the path to the selected database file. The path can be edited manually.  
  
     **Message**  
     Displays either a blank message or a "**File not found**" hyperlink.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
### <a name="to-attach-a-database"></a>Per collegare un database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Usare l'istruzione [CREATE DATABASE](../../t-sql/statements/create-database-sql-server-transact-sql.md) con la clausola `FOR ATTACH`.  
  
     Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si collegano i file del database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e si rinomina il database in `MyAdventureWorks`.  
  
    ```sql  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
    ```  
  
    > [!NOTE]  
    > In alternativa, è possibile usare la stored procedure [sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) o [sp_attach_single_file_db](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md) . Tuttavia, queste stored procedure verranno eliminate nelle versioni future di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. È consigliabile utilizzare `CREATE DATABASE ... FOR ATTACH` in alternativa.  
  
##  <a name="FollowUp"></a> Completamento: Dopo l'aggiornamento di un database di SQL Server  
Una volta aggiornato utilizzando il metodo di collegamento, il database viene reso immediatamente disponibile e viene aggiornato automaticamente. Se il database include indici full-text, questi vengono importati, reimpostati o ricompilati dal processo di aggiornamento, a seconda dell'impostazione della proprietà del server **Opzione di aggiornamento full-text** . Se l'opzione di aggiornamento è impostata su **Importa** o **Ricompila**, gli indici full-text non saranno disponibili durante l'aggiornamento. A seconda della quantità di dati indicizzati, l'importazione può richiedere diverse ore, mentre la ricompilazione può risultare dieci volte più lunga. Si noti anche che, quando l'opzione di aggiornamento è impostata su **Importa**e un catalogo full-text non è disponibile, gli indici full-text associati vengono ricompilati.  
  
Se il livello di compatibilità di un database utente è 100 o superiore prima dell'aggiornamento, rimane invariato dopo l'aggiornamento. Se il livello di compatibilità è 90 prima dell'aggiornamento, nel database aggiornato viene impostato su 100, ovvero sul livello di compatibilità supportato più basso in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
> [!NOTE]
> Se si collega un database da un'istanza che esegue [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] o versioni precedenti con Change Data Capture (CDC) abilitato, è necessario eseguire anche il comando seguente per aggiornare i metadati di Change Data Capture (CDC).
  
```sql
USE <database name>
EXEC sys.sp_cdc_vupgrade  
``` 
 
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) 
 <br>[Gestire i metadati quando si rende disponibile un database in un altro server](manage-metadata-when-making-a-database-available-on-another-server.md)  
 [Scollegamento di un database](../../relational-databases/databases/detach-a-database.md)  
  
  
