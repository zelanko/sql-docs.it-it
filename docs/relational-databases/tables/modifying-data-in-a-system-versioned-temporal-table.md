---
title: Modifica dei dati in una tabella temporale con controllo delle versioni di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 92b1b2098d1486c8dbc6958c9668387c815047d8
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403446"
---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>Modifica dei dati in una tabella temporale con controllo delle versioni di sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  È possibile modificare i dati in una tabella temporale con controllo delle versioni di sistema usando istruzioni DML regolari, tenendo però presente che i dati della colonna periodo non possono essere modificati direttamente. Quando i dati vengono aggiornati, sono sottoposti al controllo delle versioni e la versione precedente di ogni riga aggiornata viene inserita nella tabella di cronologia. Quando vengono eliminati, l'eliminazione è logica e la riga viene spostata dalla tabella corrente alla tabella di cronologia senza che i dati siano eliminati definitivamente.  
  
## <a name="inserting-data"></a>Inserimento di dati  
 Quando si inseriscono nuovi dati è necessario tenere conto delle colonne **PERIOD** se non sono **HIDDEN**. Nelle tabelle temporali con controllo delle versioni di sistema è anche possibile usare il cambio della partizione.  
  
### <a name="insert-new-data-with-visible-period-columns"></a>Inserire nuovi dati con colonne periodo visibili  
 È possibile costruire l’istruzione **INSERT** quando si hanno colonne **PERIOD** visibili come le seguenti, per tenere conto delle nuove colonne **PERIOD** :  
  
-   Se si specifica l'elenco delle colonne nell’istruzione **INSERT** , è possibile omettere le colonne **PERIOD** , perché il sistema genera automaticamente i relativi valori.  
  
    ```  
    --Insert with column list and without period columns   
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID])   
    VALUES(10, 'Marketing', 101, 1);  
  
    ```  
  
-   Se si specificano le colonne**PERIOD** nell'elenco colonne nell’istruzione **INSERT** , è necessario specificare anche **DEFAULT** come relativo valore.  
  
    ```  
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID], SysStartTime, SysEndTime)   
    VALUES(11, 'Sales', 101, 1, default, default);  
  
    ```  
  
-   Se non si specifica l'elenco colonne nell’istruzione **INSERT** , specificare **DEFAULT** per le colonne **PERIOD** .  
  
    ```  
    --Insert without  column list and DEFAULT values for period columns   
    INSERT INTO [dbo].[Department]    
    VALUES(12, 'Production', 101, 1, default, default);  
  
    ```  
  
### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>Inserire dati in una tabella con colonne periodo HIDDEN  
 Se le colonne **PERIOD** vengono specificate come HIDDEN, quando si utilizza l’istruzione INSERT è necessario indicare solo i valori per le colonne visibili, senza specificare l'elenco colonne. Non è necessario tenere conto delle nuove colonne **PERIOD** nell’istruzione **INSERT** . In questo modo le applicazioni legacy continueranno a funzionare quando si abilita il controllo delle versioni di sistema nelle tabelle a cui verrà applicata la funzionalità.  
  
```  
CREATE TABLE [dbo].[CompanyLocation]  
(   
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY  
   , [LocName] [varchar](50) NOT NULL  
   , [City] [varchar](50) NOT NULL  
   , [SysStartTime] [datetime2](0) GENERATED ALWAYS AS ROW START HIDDEN NOT NULL   
   , [SysEndTime] [datetime2](0) GENERATED ALWAYS AS ROW END HIDDEN NOT NULL   
   , PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])   
)    
WITH ( SYSTEM_VERSIONING = ON );   
GO   
INSERT INTO [dbo].[CompanyLocation]   
VALUES  ('Headquarters', 'New York');  
  
```  
  
### <a name="inserting-data-using-partition-switch"></a>Inserimento di dati con PARTITION SWITCH  
 Se la tabella corrente è partizionata è possibile usare il cambio di partizione per caricare in modo efficiente i dati in una partizione vuota oppure su più partizioni in parallelo.   
La tabella di staging usata nell'istruzione **PARTITION SWITCH IN** con una tabella temporale con controllo delle versioni di sistema deve avere la definizione di **SYSTEM_TIME PERIOD**, ma non deve essere necessariamente una tabella temporale con controllo delle versioni di sistema.    
Ciò assicura l’esecuzione di controlli di coerenza temporale durante l'inserimento di dati in una tabella di staging o quando il periodo SYSTEM_TIME viene aggiunto a una tabella di staging già popolata.  
  
```  
/*Create staging table with period definition for SWITCH IN temporal table*/   
CREATE TABLE [dbo].[Staging_Department_Partition2]  
(   
     [DeptID] [int] NOT NULL  
   , [DeptName] [varchar](50)  NOT NULL  
   , [ManagerID] [int] NULL  
   , [ParentDeptID] [int] NULL  
   , [SysStartTime] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
   , [SysEndTime] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )   
) ON [PRIMARY]   
  
/*Create aligned primary key*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
ADD CONSTRAINT [Staging_Department_Partition2_PK]  
   PRIMARY KEY CLUSTERED  
   (  [DeptID] ASC )     
   ON [PRIMARY]   
  
/*   
Create and enforce constraints for partition boundaries.   
Partition 2 contains rows with DeptID > 100 and DeptID <=200   
*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]      
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]     
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
   CHECK CONSTRAINT [chk_staging_Department_partition_2]   
  
/*Load data into staging table*/   
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])   
VALUES (101,'D101',1,NULL)  
  
/*Use PARTITION SWITCH IN to efficiently add data to current table */    
ALTER TABLE [Staging_Department]    
SWITCH TO [dbo].[Department] PARTITION 2;  
  
```  
  
 Se si tenta di eseguire l'istruzione PARTITION SWITCH da una tabella priva di definizione del periodo verrà visualizzato il messaggio di errore: `Msg 13577, Level 16, State 1, Line 25    ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`  
  
## <a name="updating-data"></a>Aggiornamento dati  
 I dati nella tabella corrente vengono aggiornati con una normale istruzione **UPDATE** . È possibile aggiornare i dati nella tabella corrente dalla tabella di cronologia per lo scenario "oops". Non è tuttavia possibile aggiornare le colonne **PERIOD** né aggiornare direttamente i dati nella tabella di cronologia se **SYSTEM_VERSIONING = ON**.   
Impostare **SYSTEM_VERSIONING = OFF** e aggiornare le righe dalla tabella corrente e di cronologia, tenendo presente che in questo modo il sistema non conserverà la cronologia delle modifiche.  
  
### <a name="updating-the-current-table"></a>Aggiornamento della tabella corrente  
 In questo esempio, la colonna ManagerID viene aggiornata per ogni riga in cui DeptID = 10. Non c’è alcun riferimento alle colonne **PERIOD** .  
  
```  
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10  
```  
  
 Tuttavia, non è possibile aggiornare una colonna **PERIOD** né la tabella di cronologia.  In questo esempio, il tentativo di aggiornare una colonna **PERIOD** genera un errore.  
  
```  
UPDATE [dbo].[Department]    
SET SysStartTime = '2015-09-23 23:48:31.2990175'    
WHERE DeptID = 10 ;  
  
Msg 13537, Level 16, State 1, Line 3   
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.  
  
```  
  
### <a name="updating-the-current-table-from-the-history-table"></a>Aggiornamento della tabella corrente dalla tabella di cronologia  
 È possibile usare l'istruzione **UPDATE** nella tabella corrente per ripristinare lo stato corrente della riga a uno specifico stato valido precedente (ripristino all'ultima versione di riga valida nota). Nell'esempio seguente i valori nella tabella di cronologia vengono ripristinati al 25-04-2015, quando DeptID = 10.  
  
```  
UPDATE Department   
SET DeptName = History.DeptName   
FROM Department    
FOR SYSTEM_TIME AS OF '2015-04-25' AS History   
WHERE History.DeptID  = 10   
AND Department.DeptID = 10 ;  
  
```  
  
## <a name="deleting-data"></a>Eliminazione di dati  
 È possibile eliminare dati dalla tabella corrente con una normale istruzione **DELETE** . La colonna periodo finale delle righe eliminate verrà popolata con l'ora di inizio della transazione sottostante.   
Non è possibile eliminare direttamente le righe dalla tabella di cronologia se **SYSTEM_VERSIONING = ON**.   
Impostare **SYSTEM_VERSIONING = OFF** ed eliminare le righe dalla tabella corrente e di cronologia, tenendo presente che in questo modo il sistema non conserverà la cronologia delle modifiche.   
Le istruzioni**TRUNCATE**, **SWITCH PARTITION OUT** della tabella corrente e l'istruzione **SWITCH PARTITION IN** della tabella di cronologia non sono supportate se **SYSTEM_VERSIONING = ON**.  
  
## <a name="using-merge-to-modify-data-in-temporal-table"></a>Utilizzo di MERGE per modificare i dati in una tabella temporale  
 L’operazione**MERGE** è supportata con le stesse limitazioni delle istruzioni **INSERT** e **UPDATE** relativamente alle colonne **PERIOD** .  
  
```  
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));   
GO   
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');   
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');   
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');   
  
MERGE dbo.Department AS target   
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)   
ON (target.DeptId = source.DeptId)   
WHEN MATCHED THEN    
    UPDATE   
   SET DeptName = source.DeptName   
WHEN NOT MATCHED THEN   
   INSERT (DeptName)   
   VALUES (source.DeptName);  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)   
 [Creazione di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Modifica dello schema di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Arresto del controllo delle versioni di sistema in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
