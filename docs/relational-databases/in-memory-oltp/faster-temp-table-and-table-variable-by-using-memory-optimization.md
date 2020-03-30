---
title: Ottimizzazione della memoria per tabella temporanea e variabile di tabella più rapide
ms.custom: seo-dt-2019
ms.date: 06/01/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
author: Jodebrui
ms.author: jodebrui
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 833108cfc5e8a11f72e8b7cb7b628690b0050c58
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412684"
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>Tabella temporanea e variabile di tabella più rapide con l'ottimizzazione per la memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Se si usano tabelle temporanee, variabili di tabella o parametri con valori di tabella, è possibile convertirli per usufruire delle tabelle e delle variabili di tabella ottimizzata per la memoria per migliorare le prestazioni. Le modifiche al codice sono in genere limitate.  
  
L'articolo illustra:  
  
- Scenari a sostegno della conversione in elementi in memoria.  
- Passaggi tecnici per l'implementazione della conversione in elementi in memoria.  
- Prerequisiti per la conversione in elementi in memoria.  
- Un esempio di codice che evidenzia i vantaggi in termini di prestazioni dell'ottimizzazione per la memoria
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>R. Introduzione alle variabili di tabella ottimizzata per la memoria  
  
Una variabile di tabella ottimizzata per la memoria offre una maggiore efficienza grazie all'uso dello stesso algoritmo e delle stesse strutture di dati ottimizzati per la memoria usati dalle tabelle ottimizzate per la memoria. L'efficienza è particolarmente evidente quando viene eseguito l'accesso alla variabile di tabella dall'interno di un modulo compilato in modo nativo.  
  
  
Una variabile di tabella ottimizzata per la memoria:  
  
- È archiviata solo in memoria e non ha alcun componente su disco.  
- Non comporta alcuna attività di I/O.  
- Non comporta alcun utilizzo di tempdb o contesa.  
- Può essere passata in una stored procedure come parametro con valori di tabella (TVP).  
- Deve avere almeno un indice, hash o non cluster.  
  - Per un indice hash, il numero di bucket dovrebbe essere idealmente 1 o 2 volte il numero di chiavi di indice univoco previsto. Tuttavia, sovrastimare il numero di bucket è solitamente corretto (fino a 10 X). Per dettagli, vedere [Indexes for Memory-Optimized Tables](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)(Indici per tabelle con ottimizzazione per la memoria).  

  
  
#### <a name="object-types"></a>Tipi di oggetto  
  
OLTP in memoria offre gli oggetti seguenti che possono essere usati per l'ottimizzazione per la memoria di tabelle temporanee e variabili di tabella:  
  
- Tabelle ottimizzate per la memoria  
  - Durability = SCHEMA_ONLY  
- Variabili di tabella con ottimizzazione per la memoria  
  - Devono essere dichiarate in due passaggi (anziché inline):  
    - `CREATE TYPE my_type AS TABLE ...;` , quindi  
    - `DECLARE @mytablevariable my_type;`.  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>B. Scenario: sostituire la tabella temporanea globale  
  
La sostituzione di una tabella temporanea globale con una tabella SCHEMA_ONLY con ottimizzazione per la memoria è piuttosto semplice. La principale modifica consiste nel creare la tabella in fase di distribuzione, non in fase di esecuzione. La creazione di tabelle con ottimizzazione per la memoria richiede più tempo rispetto alla creazione di tabelle tradizionali, a causa delle ottimizzazioni in fase di compilazione. La creazione e il rilascio di tabelle con ottimizzazione per la memoria come parte del carico di lavoro online influirebbe sulle prestazioni del carico di lavoro, nonché sulle prestazioni della fase di rollforward nei database secondari AlwaysOn e nel ripristino del database.

Si supponga di avere la tabella temporanea globale seguente.  
  
  
```sql
CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
```
  
  
  
È possibile sostituire la tabella temporanea globale con la tabella ottimizzata per la memoria seguente che include DURABILITY = SCHEMA_ONLY.  
  
  
  
```sql
CREATE TABLE dbo.soGlobalB  
(  
    Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
    Column2   NVARCHAR(4000)  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
        DURABILITY        = SCHEMA_ONLY);  
```  
  
  
  
#### <a name="b1-steps"></a>B.1 Passaggi  
  
Per convertire la tabella temporanea globale in SCHEMA_ONLY, eseguire i passaggi seguenti:  
  
  
1. Creare la tabella **dbo.soGlobalB**, una sola volta, allo stesso modo di una normale tabella su disco.  
2. Rimuovere da Transact-SQL la creazione della tabella **&#x23;&#x23;tempGlobalB**.  È importante creare la tabella con ottimizzazione per la memoria in fase di distribuzione, non in fase di esecuzione, per evitare il sovraccarico di compilazione associato alla creazione della tabella.
3. In T-SQL sostituire tutti i riferimenti di **&#x23;&#x23;tempGlobalB** con **dbo.soGlobalB**.  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>C. Scenario: sostituire la tabella temporanea di sessione  
  
Le operazioni preliminari per la sostituzione di una tabella temporanea di sessione implicano un uso maggiore di T-SQL rispetto allo scenario della tabella temporanea globale precedente. Fortunatamente, una maggior quantità di T-SQL non implica alcuna altra operazione per eseguire la conversione.  

Come nello scenario di tabelle temporanee globali, la più importante modifica consiste nella creazione della tabella in fase di distribuzione, non di runtime, per evitare il sovraccarico dovuto alla compilazione.
  
Si supponga di avere la tabella temporanea di sessione seguente.  
  
  
  
```sql  
CREATE TABLE #tempSessionC  
(  
    Column1   INT   NOT NULL ,  
    Column2   NVARCHAR(4000)  
);  
```
  
  
  
Per prima cosa creare la seguente funzione con valori di tabella per applicare un filtro in **\@\@spid**. La funzione potrà essere usata da tutte le tabelle SCHEMA_ONLY convertite da tabelle temporanee di sessione.  
  
  
  
```sql  
CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
    RETURNS TABLE  
    WITH SCHEMABINDING , NATIVE_COMPILATION  
AS  
    RETURN  
        SELECT 1 AS fn_SpidFilter  
            WHERE @SpidFilter = @@spid;  
```
  
  
  
Creare quindi la tabella SCHEMA_ONLY e i criteri di sicurezza nella tabella.  
  
  
Si noti che ogni tabella ottimizzata per la memoria deve contenere almeno un indice.  
  
- Per la tabella dbo.soSessionC potrebbe essere consigliabile un indice HASH, se viene calcolato il BUCKET_COUNT corretto. In questo esempio, tuttavia, viene usato per semplicità un indice NONCLUSTERED.  
  
  
  
```sql
CREATE TABLE dbo.soSessionC  
(  
    Column1     INT         NOT NULL,  
    Column2     NVARCHAR(4000)  NULL,  

    SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  

    INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
    --INDEX ix_SpidFilter HASH  
    --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
        
    CONSTRAINT CHK_soSessionC_SpidFilter  
        CHECK ( SpidFilter = @@spid ),  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_ONLY);  
go  
  
  
CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
    ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
    ON dbo.soSessionC  
    WITH (STATE = ON);  
go  
```  
  
  
  
Infine, nel codice T-SQL generale:  
  
1. Modificare tutti i riferimenti alla tabella temporanea nelle istruzioni Transact-SQL impostando la nuova tabella ottimizzata per la memoria:
    - _Precedente:_ &#x23;tempSessionC  
    - _Nuovo:_ dbo.soSessionC  
2. Sostituire le istruzioni `CREATE TABLE #tempSessionC` nel codice con `DELETE FROM dbo.soSessionC` per assicurarsi che una sessione non venga esposta al contenuto della tabella inserito da una sessione precedente con lo stesso session_id. È importante creare la tabella con ottimizzazione per la memoria in fase di distribuzione, non in fase di esecuzione, per evitare il sovraccarico di compilazione associato alla creazione della tabella.
3. Rimuovere le istruzioni `DROP TABLE #tempSessionC` dal codice. Facoltativamente, è possibile inserire un'istruzione `DELETE FROM dbo.soSessionC`, nel caso le dimensioni della memoria costituiscano un potenziale problema
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memory_optimizedon"></a>D. Scenario: la variabile di tabella può essere MEMORY_OPTIMIZED=ON  
  
  
Una variabile di tabella tradizionale rappresenta una tabella del database tempdb. Per ottenere migliori prestazioni è possibile convertire la variabile di tabella in variabile di tabella con ottimizzazione per la memoria.  
  
Di seguito è riportato il codice T-SQL per una variabile di tabella tradizionale. L'ambito termina alla fine del batch o della sessione.  
  
  
  
```sql
DECLARE @tvTableD TABLE  
    ( Column1   INT   NOT NULL ,  
      Column2   CHAR(10) );  
```
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D.1 Convertire da inline a esplicito  
  
La sintassi precedente crea la variabile di tabella *inline*. La sintassi inline non supporta l'ottimizzazione per la memoria. È necessario quindi convertire la sintassi inline nella sintassi esplicita per TYPE.  
  
*Ambito:* la definizione TYPE creata dal primo batch delimitato da go rimane valida anche dopo che il server è stato arrestato e riavviato. Tuttavia, dopo il primo delimitatore go, la tabella dichiarata @tvTableC rimane valida solo fino a quando non vengono raggiunti il go successivo e la fine del batch.  
  
  
  
```sql  
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
        
SET NoCount ON;  
DECLARE @tvTableD dbo.typeTableD  
;  
INSERT INTO @tvTableD (Column1) values (1), (2)  
;  
SELECT * from @tvTableD;  
go  
```
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 Convertire esplicito su disco in ottimizzato per la memoria  
  
Una variabile di tabella ottimizzata per la memoria è memorizzata in tempdb. L'ottimizzazione per la memoria offre una velocità spesso maggiore di 10 volte o più.  
  
La conversione in ottimizzato per la memoria viene eseguita in un solo passaggio. Migliorare la creazione TYPE esplicita come segue, aggiungendo:  
  
- Un indice. Si noti che ogni tabella ottimizzata per la memoria deve contenere almeno un indice.  
- MEMORY_OPTIMIZED = ON.  
  
  
  
```sql
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL   INDEX ix1,  
        Column2  CHAR(10)  
    )  
    WITH  
        (MEMORY_OPTIMIZED = ON);  
```  
  
  
  
La conversione è stata completata.  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>E. FILEGROUP prerequisito per SQL Server  
  
In Microsoft SQL Server per usare le funzionalità ottimizzate per la memoria, è necessario che il database includa un FILEGROUP dichiarato con **MEMORY_OPTIMIZED_DATA**.  
  
- Il database SQL di Azure non richiede la creazione del FILEGROUP.  
  
  
*Prerequisito:* il seguente codice Transact-SQL per un FILEGROUP è un prerequisito per i lunghi esempi di codice T-SQL riportati nelle sezioni successive di questo articolo.  
  
1. È necessario usare SSMS.exe o un altro strumento che può inviare T-SQL.  
2. Incollare il codice T-SQL di FILEGROUP di esempio in SQL Server Management Studio.  
3. Modificare il codice T-SQL per cambiare i nomi e i percorsi di directory in base alle proprie esigenze.  
  - Tutte le directory nel valore FILENAME devono essere già esistenti, ad eccezione della directory finale.  
4. Eseguire il codice T-SQL modificato.  
  - Non è necessario eseguire il FILEGROUP T-SQL più di una volta, anche nel caso in cui il codice T-SQL di confronto della velocità venga modificato e rieseguito più volte.  
  
  
  
 
```sql
ALTER DATABASE InMemTest2  
    ADD FILEGROUP FgMemOptim3  
        CONTAINS MEMORY_OPTIMIZED_DATA;  
go  
ALTER DATABASE InMemTest2  
    ADD FILE  
    (  
        NAME = N'FileMemOptim3a',  
        FILENAME = N'C:\DATA\FileMemOptim3a'  
                    --  C:\DATA\    preexisted.  
    )  
    TO FILEGROUP FgMemOptim3;  
go  
```  


Lo script seguente crea automaticamente il filegroup e configura le impostazioni di database consigliate: [enable-in-memory-oltp.sql](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/in-memory-database/in-memory-oltp/t-sql-scripts/enable-in-memory-oltp.sql)
  
Per altre informazioni su `ALTER DATABASE ... ADD` per FILE e FILEGROUP, vedere:  
  
- [Opzioni per file e filegroup ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [Filegroup con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>F. Test rapido per dimostrare il miglioramento della velocità  
  
  
Questa sezione include il codice Transact-SQL che è possibile eseguire per testare e confrontare l'aumento della velocità di INSERT-DELETE dovuto all'uso di una variabile di tabella ottimizzata per la memoria. Il codice è suddiviso in due parti pressoché uguali, ad eccezione del fatto che nella prima parte il tipo di tabella corrisponde a una tabella ottimizzata per la memoria.  
  
Il test di confronto richiede circa 7 secondi. Per eseguire l'esempio:  
  
1. *Prerequisito:* è necessario avere già eseguito il codice T-SQL di FILEGROUP della sezione precedente.  
2. Eseguire lo script INSERT-DELETE T-SQL seguente.  
  - Si noti l'istruzione 'GO 5001' che invia il codice T-SQL 5001 volte. È possibile modificare il numero ed eseguire di nuovo lo script.  
  
Quando si esegue lo script in un database SQL di Azure, assicurarsi di eseguire lo script da una macchina virtuale nella stessa area.

  
```sql
PRINT ' ';  
PRINT '---- Next, memory-optimized, faster. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  
CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
        AS TABLE  
        (  
            Column1  INT NOT NULL INDEX ix1,  
            Column2  CHAR(10)  
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _mem.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  

---- End memory-optimized.  
-------------------------------------------------  
---- Start traditional on-disk.  

PRINT ' ';  
PRINT '---- Next, tempdb based, slower. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
    AS TABLE  
    (  
        Column1  INT NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
----  

PRINT '---- Tests done. ----';  

go  

/*** Actual output, SQL Server 2016:  

---- Next, memory-optimized, faster. ----  
2016-04-20 00:26:58.033  = Begin time, _mem.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:26:58.733  = End time, _mem.  

---- Next, tempdb based, slower. ----  
2016-04-20 00:26:58.750  = Begin time, _tempdb.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:27:05.440  = End time, _tempdb.  
---- Tests done. ----  
***/
```
  
  
  
## <a name="g-predict-active-memory-consumption"></a>G. Stimare il consumo di memoria attiva  
  
È possibile imparare a prevedere la quantità di memoria attiva richiesta dalle tabelle ottimizzate per la memoria con le risorse seguenti:  
  
- [Stimare i requisiti di memoria delle tabelle con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Dimensioni di tabelle e righe per le tabelle con ottimizzazione per la memoria: esempio di calcolo](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
Per le variabili di tabella di dimensioni maggiori, gli indici non cluster usano una maggior quantità di memoria rispetto a quella usata per le *tabelle* ottimizzate per la memoria. Maggiore è il totale delle righe e la chiave di indice, maggiore sarà la differenza.  
  
Se l'accesso alla variabile di tabella ottimizzata per la memoria avviene soltanto con un determinato valore di chiave a ogni accesso, è consigliabile usare un indice hash anziché un indice non cluster. Tuttavia, se non si è in grado di stimare il valore BUCKET_COUNT appropriato, un indice NONCLUSTERED rappresenta una buona scelta.  
  
## <a name="h-see-also"></a>H. Vedere anche  
  
- [Tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

- [Definizione di durabilità per gli oggetti con ottimizzazione per la memoria](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)

- [Aggiornamento cumulativo per eliminare errori di memoria insufficiente non corretti, annunciato nel blog settembre 2017](https://support.microsoft.com/help/4025208/fix-memory-leak-occurs-when-you-use-memory-optimized-tables-in-microso)
    - [SQL Server 2016 build versions](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) (Versioni build di SQL Server 2016) include dettagli completi su versioni, Service Pack e aggiornamenti cumulativi.
    - Questi messaggi di errore occasionali non corretti non si verificano nell'edizione Enterprise di SQL Server.

