---
description: Creazione di una tabella temporale con controllo delle versioni di sistema
title: Creazione di una tabella temporale con controllo delle versioni di sistema | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a68b5fa8944612cd4262ef97cb16c8963398dec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446503"
---
# <a name="creating-a-system-versioned-temporal-table"></a>Creazione di una tabella temporale con controllo delle versioni di sistema

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Quando si crea una tabella temporale con controllo delle versioni di sistema esistono tre modi per specificare la tabella di cronologia:

- Tabella temporale con una tabella di cronologia anonima: si specifica lo schema della tabella corrente e il sistema crea una tabella di cronologia corrispondente con un nome generato automaticamente.
- Tabella temporale con una tabella di cronologia predefinita: si specificano il nome dello schema della tabella di cronologia e il nome della tabella e il sistema crea la tabella di cronologia in quello schema.
- Tabella temporale con una tabella di cronologia definita dall'utente creata in precedenza: si crea la tabella di cronologia più adatta alle esigenze e poi si fa riferimento alla tabella durante la creazione della tabella temporale.

## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>Creazione di una tabella temporale con una tabella di cronologia anonima

Creare una tabella temporale con una tabella di cronologia "anonima" è una soluzione comoda per poter generare rapidamente oggetti, specialmente nei prototipi e negli ambienti di test. È inoltre il modo più semplice di creare una tabella temporale in quanto non richiede alcun parametro nella clausola **SYSTEM_VERSIONING**. Nell'esempio seguente viene creata una nuova tabella con il controllo delle versioni di sistema attivato, senza definire il nome della tabella di cronologia.

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON);
```

### <a name="important-remarks"></a>Note importanti

- Una tabella temporale con il controllo delle versioni di sistema deve avere una chiave primaria definita e avere esattamente un **PERIOD FOR SYSTEM_TIME** definito con due colonne datetime2, dichiarate come **GENERATED ALWAYS AS ROW START / END**
- Le colonne **PERIOD** sono sempre considerate prive di supporto per i valori Null, anche se il supporto dei valori Null non è specificato. Se le colonne **PERIOD** sono definite esplicitamente per ammettere valori Null, l'istruzione **CREATE TABLE** non sarà eseguita.
- La tabella di cronologia deve sempre essere allineata a livello di schema con la tabella corrente o la tabella temporale, in termini di numero di colonne, nomi delle colonne, ordinamento e tipi di dati.
- Una tabella di cronologia anonima viene creata automaticamente nello stesso schema della tabella corrente o della tabella temporale.
- Il nome della tabella di cronologia anonimo presenta il seguente formato: *MSSQL_TemporalHistoryFor_<current_temporal_table_object_id>_[suffisso]* . Il suffisso è facoltativo e sarà aggiunto solo se la prima parte del nome della tabella non è univoco.
- La tabella di cronologia viene creata come tabella rowstore. Se possibile, viene applicata la compressione di pagina, altrimenti la tabella di cronologia sarà non compressa. Ad esempio, alcune configurazioni di tabella, come le colonne di tipo sparse, non consentono la compressione.
- Viene creato un indice cluster predefinito per la tabella di cronologia con un nome generato automaticamente in formato *IX_<history_table_name>* . L'indice cluster contiene le colonne **PERIOD** (inizio, fine).
- Per creare la tabella corrente come una tabella ottimizzata per la memoria, vedere [Tabelle temporali con controllo delle versioni di sistema con tabelle ottimizzate per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).

## <a name="creating-a-temporal-table-with-a-default-history-table"></a>Creazione di una tabella temporale con una tabella di cronologia predefinita

Creare una tabella temporale con una tabella di cronologia predefinita è una soluzione comoda quando si vuole controllare la denominazione e al tempo stesso lasciare che sia il sistema a creare la tabella di cronologia con la configurazione predefinita. Nell'esempio seguente viene creata una nuova tabella con il controllo delle versioni di sistema attivato, definendo esplicitamente il nome della tabella di cronologia.

```sql
CREATE TABLE Department
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>Note importanti

La tabella di cronologia viene creata con le stesse regole valide per la creazione di una tabella di cronologia "anonima", inoltre si applicano le seguenti regole specifiche alla tabella di cronologia denominata.

- Il nome dello schema è obbligatorio per il parametro **HISTORY_TABLE** .
- Se lo schema specificato non esiste, l'istruzione **CREATE TABLE** non verrà seguita.
- Se la tabella specificata dal parametro **HISTORY_TABLE** esiste già, sarà convalidata rispetto alla nuova tabella temporale che viene creata in termini di [coerenza dello schema e coerenza dei dati temporali](https://msdn.microsoft.com/library/dn935015.aspx). Se si specifica una tabella di cronologia non valida, l'istruzione **CREATE TABLE** non verrà eseguita.

## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>Creazione di una tabella temporale con una tabella di cronologia definita dall'utente

Creare una tabella temporale con una tabella di cronologia definita dall'utente è una soluzione comoda quando l'utente vuole specificare la tabella di cronologia con determinate opzioni di archiviazione e indici aggiuntivi. Nell'esempio seguente viene creata una tabella di cronologia definita dall'utente con uno schema allineato con la tabella temporale che verrà creata. Per questa tabella di cronologia definita dall'utente vengono creati un indice columnstore cluster e un indice rowstore non cluster (albero B) aggiuntivo per le ricerche di punti. Dopo la creazione di questa tabella di cronologia definita dall'utente, viene creata la tabella temporale con controllo delle versioni di sistema specificando la tabella di cronologia definita dall'utente come tabella di cronologia predefinita.

```sql
CREATE TABLE DepartmentHistory
(
    DeptID INT NOT NULL
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 NOT NULL
  , SysEndTime DATETIME2 NOT NULL
);
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory
    ON DepartmentHistory;
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS
    ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);
GO

CREATE TABLE Department
(
    DeptID int NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```

### <a name="important-remarks"></a>Note importanti

- Se si prevede di eseguire query analitiche sui dati storici che impiegano funzioni di aggregazione o suddivisione in finestre, si consiglia vivamente di creare un indice columnstore cluster come indice primario per la compressione dei dati e le prestazioni delle query.
- Se il caso d'uso principale è il controllo dei dati (ovvero la ricerca di modifiche nella cronologia per una singola riga della tabella corrente), è consigliabile creare una tabella di cronologia rowstore con un indice cluster
- La tabella di cronologia non può avere una chiave primaria, chiavi esterne, indici univoci, vincoli di tabella e neppure trigger. Non può essere configurata per Change Data Capture, rilevamento delle modifiche, replica transazionale o replica di tipo merge.

## <a name="alter-non-temporal-table-to-be-a-system-versioned-temporal-table"></a>Modificare una tabella non temporale per trasformarla in una tabella temporale con controllo delle versioni di sistema

Quando è necessario attivare il controllo delle versioni di sistema usando una tabella esistente, come quando si vuole eseguire la migrazione di una soluzione temporale personalizzata al supporto incorporato.
Ad esempio, si potrebbe avere un set di tabelle in cui il controllo delle versioni è implementato mediante trigger. L'uso del controllo delle versioni di sistema temporale è meno complesso e offre vantaggi aggiuntivi fra cui:

- Cronologia non modificabile
- Nuova sintassi per le query con spostamento cronologico
- Prestazioni DML ottimizzate
- Costi di manutenzione minimi

 Quando si converte una tabella esistente, è consigliabile usare la clausola **HIDDEN** per nascondere le nuove colonne **PERIOD** (le colonne datetime2 **SysStartTime** e **SysEndTime**) al fine di evitare conseguenze sulle applicazioni esistenti che non specificano esplicitamente i nomi delle colonne (ad es. SELECT * o INSERT senza elenco delle colonne) o non sono progettate per gestire nuove colonne.

### <a name="adding-versioning-to-non-temporal-tables"></a>Aggiunta del controllo delle versioni a tabelle non temporali

Se si vuole iniziare a monitorare le modifiche di una tabella non temporale che contiene i dati, è necessario aggiungere la definizione **PERIOD** e facoltativamente specificare un nome per una tabella di cronologia vuota che sarà creata da SQL Server:

```sql
CREATE SCHEMA History;
GO

ALTER TABLE InsurancePolicy
    ADD
        SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START HIDDEN
            CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()
      , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END HIDDEN
            CONSTRAINT DF_SysEnd DEFAULT CONVERT(DATETIME2, '9999-12-31 23:59:59.9999999'),
        PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);
GO

ALTER TABLE InsurancePolicy
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy));
```

> [!IMPORTANT]
> La precisione per DATETIME2 deve allinearsi con la precisione per la tabella sottostante. Vedere le osservazioni seguenti.

#### <a name="important-remarks"></a>Note importanti

- L'aggiunta di colonne che non supportano i valori Null con valori predefiniti a una tabella esistente contenente dati corrisponde a un'operazione di dimensionamento dei dati in tutte le edizioni eccetto SQL Server Enterprise Edition (in cui corrisponde a un'operazione di metadati). Con una tabella di cronologia esistente di grandi dimensioni contenente dati in SQL Server Standard Edition, aggiungere una colonna che non supporta i valori Null può essere un'operazione costosa.
- I vincoli per le colonne di inizio e fine periodo devono essere scelti attentamente:
  - Il valore predefinito per la colonna di inizio specifica da che punto nel tempo le righe esistenti sono considerate valide. Non può essere specificato come valore datetime futuro.
  - L'ora di fine deve essere specificata come valore massimo per una determinata precisione datetime2, ad esempio `9999-12-31 23:59:59` o `9999-12-31 23:59:59.9999999`.
- Se si aggiunge Period, verranno eseguiti controlli di coerenza sulla tabella corrente per garantire che i valori predefiniti per le colonne di period siano validi.
- Se viene specificata una tabella di cronologia esistente quando si attiva **SYSTEM_VERSIONING**, sarà eseguito un controllo di coerenza sui dati nella tabella corrente e nella tabella di cronologia. Può essere ignorato se si specifica **DATA_CONSISTENCY_CHECK = OFF** come parametro aggiuntivo.

### <a name="migrate-existing-tables-to-built-in-support"></a>Eseguire la migrazione di tabelle esistenti al supporto incorporato

Questo esempio mostra come migrare una soluzione esistente basata su trigger al supporto temporale incorporato. In questo esempio si presuppone che la soluzione personalizzata corrente suddivida i dati attuali e cronologici in due tabelle utente separate (**ProjectTaskCurrent** e **ProjectTaskHistory**). Se la soluzione esistente usa una singola tabella per archiviare le righe attuali e cronologiche, è necessario suddividere i dati in due tabelle prima di eseguire i passaggi della migrazione illustrati in questo esempio:

```sql
/*Drop trigger on future temporal table*/
DROP TRIGGER ProjectCurrent_OnUpdateDelete;
/*Make sure that future period columns are non-nullable*/
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;
ALTER TABLE ProjectTaskCurrent
    ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])
ALTER TABLE ProjectTaskCurrent
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON));
```

#### <a name="important-remarks"></a>Note importanti

- Facendo riferimento a colonne esistenti nella definizione di **PERIOD** viene modificato implicitamente generated_always_type in **AS_ROW_START** e **AS_ROW_END** per queste colonne.
- Se si aggiunge **PERIOD** verrà eseguito un controllo di coerenza dei dati sulla tabella corrente per garantire che i valori esistenti per le colonne di Period siano validi
- È consigliabile impostare **SYSTEM_VERSIONING** con **DATA_CONSISTENCY_CHECK = ON** per eseguire i controlli di coerenza dei dati sui dati esistenti.
- Se si preferiscono colonne nascoste, usare il comando `ALTER TABLE [tableName] ALTER COLUMN [columnName] ADD HIDDEN;`.

## <a name="next-steps"></a>Passaggi successivi

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
 [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
- [Modifica dei dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Modifica dello schema di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Arresto del controllo delle versioni di sistema in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
