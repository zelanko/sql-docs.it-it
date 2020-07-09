---
title: Numeri di sequenza | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0fc2167d4dc6179b760cfe03ad380b98d041f7b3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725907"
---
# <a name="sequence-numbers"></a>Numeri di sequenza
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Una sequenza è un oggetto associato a schema definito dall'utente che genera una sequenza di valori numerici in base alla specifica con la quale è stata creata la sequenza. La sequenza di valori numerici viene generata in ordine crescente o decrescente a un intervallo definito e può essere ripetuta (ciclicamente) in base alle esigenze. Le sequenze, a differenza delle colonne di identità, non sono associate a tabelle. In un'applicazione viene fatto riferimento a un oggetto sequenza per recuperare il relativo valore successivo. La relazione tra sequenze e tabelle è controllata dall'applicazione. È possibile che nelle applicazioni utente si faccia riferimento a un oggetto sequenza e vengano coordinate le chiavi dei valori di più righe e tabelle.  
  
 Una sequenza viene creata indipendentemente delle tabelle usando l'istruzione **CREATE SEQUENCE** . Le opzioni consentono di controllare i valori di incremento, massimo e minimo, il punto iniziale, la funzionalità di riavvio automatico e la memorizzazione nella cache per migliorare le prestazioni. Per informazioni sulle opzioni, vedere [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 A differenza dei valori delle colonne di identità, che vengono generati quando si inseriscono righe, un'applicazione può ottenere il numero di sequenza successivo prima di inserire la riga chiamando la funzione [NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md) . Il numero di sequenza viene allocato quando viene chiamata tale funzione, anche se il numero non viene mai inserito in una tabella. La funzione NEXT VALUE FOR può essere utilizzata come valore predefinito per una colonna in una definizione della tabella. Usare [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) per ottenere un intervallo di numeri di sequenza.  
  
 Una sequenza può essere definita come qualsiasi tipo di dati integer. Se il tipo di dati non viene specificato, viene usata per impostazione predefinita la sequenza **bigint**.  
  
## <a name="using-sequences"></a>Utilizzo di sequenze  
 Utilizzare sequenze anziché colonne di identità negli scenari seguenti:  
  
-   Nell'applicazione è richiesto un numero prima che venga effettuato l'inserimento nella tabella.  
  
-   Nell'applicazione è richiesta la condivisione di una singola serie di numeri tra più tabelle o più colonne all'interno di una tabella.  
  
-   Nell'applicazione deve essere riavviata la serie di numeri quando viene raggiunto un numero specificato. Dopo che sono stati assegnati valori da 1 a 10, ad esempio, viene iniziata di nuovo l'assegnazione di valori da 1 a 10.  
  
-   Nell'applicazione è richiesto l'ordinamento dei valori di sequenza in base a un altro campo. Dalla funzione NEXT VALUE FOR può essere applicata la clausola OVER alla chiamata di funzione. La clausola OVER garantisce che i valori restituiti vengano generati in base all'ordine della clausola ORDER BY della clausola OVER.  
  
-   In un'applicazione è richiesta l'assegnazione contemporanea di più numeri. Devono essere riservati, ad esempio, cinque numeri sequenziali. La richiesta di valori di identità potrebbe comportare gap nella serie se sono stati emessi contemporaneamente numeri per altri processi. Una chiamata a sp_sequence_get_range consente di recuperare contemporaneamente diversi numeri della sequenza.  
  
-   È necessario modificare la specifica della sequenza, ad esempio il valore di incremento.  
  
## <a name="limitations"></a>Limitazioni  
 A differenza delle colonne di identità, i cui valori non possono essere modificati, i valori di sequenza non sono protetti automaticamente dopo l'inserimento nella tabella. Per evitare la modifica dei valori di sequenza, utilizzare un trigger di aggiornamento sulla tabella per eseguire il rollback delle modifiche.  
  
 L'univocità non viene applicata automaticamente per i valori di sequenza. Da progettazione, i valori di sequenza possono essere riutilizzati. Se è necessario che i valori di sequenza in una tabella siano univoci, creare un indice univoco nella colonna. Se è necessario che i valori di sequenza in una tabella siano univoci per un gruppo di tabelle, creare trigger per impedire duplicati a causa di istruzioni di aggiornamento o ripetizione di numeri di sequenza.  
  
 L'oggetto sequenza genera numeri in base alla definizione, ma non controlla come vengono utilizzati i numeri. Nei numeri di sequenza inseriti in una tabella possono essere presenti gap quando viene eseguito il rollback di una transazione, quando un oggetto sequenza è condiviso da più tabelle o quando i numeri di sequenza vengono allocati senza essere utilizzati nelle tabelle. In caso di creazione con l'opzione CACHE, un arresto imprevisto quale un'interruzione dell'alimentazione, può provocare la perdita dei numeri di sequenza nella cache.  
  
 Se sono presenti più istanze della funzione **NEXT VALUE FOR** che specificano lo stesso generatore di sequenze in un'unica istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] , tutte le istanze restituiscono lo stesso valore per una determinata riga elaborata da questa istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Questo comportamento è coerente con lo standard ANSI.  
 
 I numeri di sequenza vengono generati esternamente all'ambito della transazione corrente. Vengono utilizzati sia in caso di commit che di rollback della transazione che utilizza il numero di sequenza. La convalida dei duplicati viene eseguita solo quando un record è completamente popolato. Ciò può provocare, in alcuni casi, l'assegnazione di uno stesso numero a più di un record durante la creazione, ma il numero viene comunque identificato come duplicato. Se si verifica questo errore e ai record successivi sono stati applicati altri valori di numerazione automatica, può verificarsi uno scarto tra i valori di numerazione automatica.
  
## <a name="typical-use"></a>Utilizzo tipico  
 Per creare un numero di sequenza intero che viene incrementato di 1 da -2.147.483.648 a 2.147.483.647, utilizzare l'istruzione seguente.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 Per creare un numero di sequenza intero simile a una colonna di identità che viene incrementato di 1 da 1 a 2.147.483.647, utilizzare l'istruzione seguente.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>Gestione di sequenze  
 Per informazioni sulle sequenze, eseguire una query su [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
 Altri esempi sono disponibili negli argomenti [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md), [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md) e [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md).  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>R. Utilizzo di un numero di sequenza in una singola tabella  
 Nell'esempio seguente viene creato uno schema denominato Test, una tabella denominata Orders e una sequenza denominata CountBy1, quindi vengono inserite righe nella tabella usando la funzione NEXT VALUE FOR.  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. Chiamata a NEXT VALUE FOR prima di inserire una riga  
 Utilizzando la tabella `Orders` creata nell'esempio A, nell'esempio seguente viene dichiarata una variabile denominata `@nextID`, quindi viene utilizzata la funzione NEXT VALUE FOR per impostare la variabile sul successivo numero di sequenza disponibile. Si presuppone che nell'applicazione vengano eseguite alcune operazioni di elaborazione dell'ordine, ad esempio fornire al cliente il numero di `OrderID` dell'ordine potenziale, quindi convalidare l'ordine. Indipendentemente dalla durata di tale elaborazione o dal numero di ordini aggiunti durante il processo, viene mantenuto il numero originale per l'utilizzo da parte di questa connessione. Infine, viene aggiunto l'ordine alla tabella `INSERT` tramite l'istruzione `Orders` .  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. Utilizzo di un numero di sequenza in più tabelle  
 In questo esempio si presuppone che un processo di controllo di una linea di produzione riceva notifica di eventi che si verificano in tutta l'officina. Ogni evento riceve un numero `EventID` univoco e a incremento progressivo costante. Per tutti gli eventi viene utilizzato lo stesso numero di sequenza `EventID` , in modo che nei report in cui vengono combinati tutti gli eventi sia possibile identificare in modo univoco ogni evento. I dati degli eventi vengono tuttavia archiviati in tre tabelle diverse, a seconda del tipo di evento. L'esempio di codice illustra come creare uno schema denominato `Audit`, una sequenza denominata `EventCounter`e tre tabelle, ciascuna delle quali usa la sequenza `EventCounter` come valore predefinito. Nell'esempio vengono quindi aggiunte righe alle tre tabelle e vengono eseguite query sui risultati.  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. Generazione di numeri di sequenza ripetuti in un set di risultati  
 Nell'esempio seguente vengono illustrate due caratteristiche dei numeri di sequenza: ripetizione e utilizzo di `NEXT VALUE FOR` in un'istruzione Select.  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. Generazione di numeri di sequenza per un set di risultati tramite la clausola OVER  
 Nell'esempio seguente viene utilizzata la clausola `OVER` per ordinare il set di risultati in base a `Name` prima che venga aggiunta la colonna di numeri di sequenza.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. Reimpostazione del numero di sequenza  
 Nell'esempio E sono stati utilizzati i primi 79 numeri di sequenza `Samples.IDLabel`. È possibile che la versione in uso di `AdventureWorks2012` restituisca un numero di risultati diverso. Eseguire gli elementi seguenti per utilizzare i successivi 79 numeri di sequenza (da 80 a 158).  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 Eseguire l'istruzione seguente per riavviare la sequenza `Samples.IDLabel`.  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 Eseguire di nuovo l'istruzione SELECT per verificare che la sequenza `Samples.IDLabel` sia ripartita dal numero 1.  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. Modifica di una tabella da identità a sequenza  
 Nell'esempio seguente vengono creati uno schema e una tabella contenente tre righe per l'esempio. Viene quindi aggiunta una nuova colonna e viene eliminata la colonna precedente.  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] che utilizzano `SELECT *` riceveranno la nuova colonna come ultima colonna anziché come prima. Se ciò non è accettabile, sarà necessario creare una tabella completamente nuova, spostare i dati in tale tabella, quindi ricreare le autorizzazioni nella nuova tabella.  
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)  
  
 [IDENTITY &#40;proprietà&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
  
  
