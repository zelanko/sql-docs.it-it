---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 6/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4409d67e60fd4d82d339ac31e96ca75b578171fe
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402816"
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Crea una tabella esterna per PolyBase o query di database elastico. In base allo scenario, la sintassi è notevolmente diversa. Una tabella esterna creata per PolyBase non può essere usata per query di database elastico.  Analogamente, una tabella esterna creata per le query di database elastico non può essere usata per PolyBase e così via. 
  
> [!NOTE]  
>  PolyBase è supportata solo in SQL Server 2016 (o versioni successive), Azure SQL Data Warehouse e Parallel Data Warehouse. Le query di database elastico sono supportate solo nel database SQL di Azure v12 o versioni successive.  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa le tabelle esterne per accedere ai dati archiviati in un cluster Hadoop o un'archiviazione BLOB di Azure. Una tabella esterna PolyBase che fa riferimento ai dati archiviati in un cluster Hadoop o un'archiviazione BLOB di Azure può essere usata anche per creare una tabella esterna per le [query di database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 Usare una tabella esterna per:  
  
-   Eseguire query sui dati di Hadoop o dell'archiviazione BLOB di Azure con istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Importare e archiviare i dati da Hadoop o dall'archiviazione BLOB di Azure nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Creare una tabella esterna da usare con una query di database elastico  
     .  
     
- Importare e archiviare i dati da Azure Data Lake Store in Azure SQL Data Warehouse
  
 Vedere anche [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [DROP EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage,  
    | REJECT_VALUE = reject_value,  
    | REJECT_SAMPLE_VALUE = reject_sample_value,
    | REJECTED_ROW_LOCATION = '\REJECT_Directory'
  
}  
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name* . [ schema_name ] . | schema_name. ] *table_name*  
 Nome della tabella da creare, composto da una, due o tre parti. Per una tabella esterna, solo i metadati della tabella vengono archiviati in SQL insieme alle statistiche di base relative al file e/o alla cartella a cui si fa riferimento in Hadoop o nell'archiviazione BLOB di Azure. I dati effettivi non vengono spostati o archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 \<column_definition> [ ,...*n* ] CREATE EXTERNAL TABLE consente una o più definizioni di colonna. Sia CREATE EXTERNAL TABLE che CREATE TABLE usano la stessa sintassi per definire una colonna. Un'eccezione è che non è possibile usare DEFAULT CONSTRAINT per le tabelle esterne. Per informazioni dettagliate sulle definizioni di colonna e i relativi tipi di dati, vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [CREATE TABLE (database SQL di Azure)](https://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1).  
  
 Le definizioni di colonna, inclusi i tipi di dati e il numero di colonne, devono corrispondere ai dati nei file esterni. In caso di mancata corrispondenza, le righe di file verranno rifiutate quando si eseguono query sui dati effettivi.  
  
 LOCATION =  '*folder_or_filepath*'  
 Specifica la cartella o il percorso e il nome del file per i dati effettivi in Hadoop o nell'archiviazione BLOB di Azure. Il percorso inizia dalla directory radice, ovvero la posizione dei dati specificata nell'origine dati esterna.  


In SQL Server l'istruzione CREATE EXTERNAL TABLE crea il percorso e la cartella, se non esiste già. Quindi è possibile usare INSERT INTO per esportare i dati da una tabella di SQL Server locale a un'origine dati esterna. Per altre informazioni, vedere l'articolo relativo alle [query di PolyBase](/sql/relational-databases/polybase/polybase-queries). 

In SQL Data Warehouse e nella piattaforma di sistemi analitici l'istruzione [CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) crea il percorso e la cartella, se non esiste. In questi due prodotti CREATE EXTERNAL TABLE non crea il percorso e la cartella.

  
 Se si specifica che LOCATION deve essere una cartella, una query PolyBase che effettua selezioni dalla tabella esterna recupererà i file dalla cartella e da tutte le relative sottocartelle. Proprio come Hadoop, PolyBase non restituisce le cartelle nascoste. Inoltre, non restituisce i file per cui il nome del file inizia con un carattere di sottolineatura (_) o un punto (.).  
  
 In questo esempio, se LOCATION='/webdata/', una query PolyBase restituisce le righe da mydata.txt e mydata2.txt.  Non restituirà mydata3.txt perché è una sottocartella di una cartella nascosta. Non restituirà _hidden.txt perché è un file nascosto.  
  
 ![Dati ricorsivi per tabelle esterne](../../t-sql/statements/media/aps-polybase-folder-traversal.png "Dati ricorsivi per tabelle esterne")  
  
 Per modificare l'impostazione predefinita e leggere solo dalla directory radice, impostare l'attributo \<polybase.recursive.traversal > su 'false' nel file di configurazione core-site.xml. Questo file si trova in `<SqlBinRoot>\PolyBase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`. Ad esempio, `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`.  
  
 DATA_SOURCE = *external_data_source_name*  
 Specifica il nome dell'origine dati esterna che contiene il percorso dei dati esterni. Questo percorso è un cluster Hadoop o un'archiviazione BLOB di Azure. Per creare un'origine dati esterna, usare [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 Specifica il nome dell'oggetto formato di file esterno che contiene il tipo di file e il metodo di compressione per i dati esterni. Per creare un formato di file esterno, usare [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 Opzioni di rifiuto  
 È possibile specificare i parametri di rifiuto che determinano in che modo PolyBase gestirà i record *dirty* che recupera dall'origine dati esterna. Un record di dati è considerato "dirty" se i tipi di dati effettivi o il numero di colonne non corrispondono alle definizioni di colonna della tabella esterna.  
  
 Se non si specificano o si modificano i valori di rifiuto, PolyBase usa i valori predefiniti. Queste informazioni sui parametri di rifiuto vengono archiviate come metadati aggiuntivi quando si crea una tabella esterna con l'istruzione CREATE EXTERNAL TABLE.   Quando una futura istruzione SELECT futuri o SELECT INTO SELECT seleziona i dati dalla tabella esterna, PolyBase usa le opzioni di rifiuto per determinare il numero o la percentuale di righe che possono essere rifiutate prima che la query effettiva non riesca. , La query restituirà risultati (parziali) finché non viene superata la soglia di rifiuto, quindi ha esito negativo con il messaggio di errore appropriato.  
  
 REJECT_TYPE = **value** | percentage  
 Chiarisce se l'opzione REJECT_VALUE è specificata come valore letterale o percentuale.  
  
 Valore  
 REJECT_VALUE è un valore letterale, non una percentuale. La query PolyBase avrà esito negativo se il numero di righe rifiutate supera *reject_value*.  
  
 Ad esempio, se REJECT_VALUE = 5 e REJECT_TYPE = value, la query SELECT di PolyBase avrà esito negativo dopo che sono state rifiutate 5 righe.  
  
 percentuale  
 REJECT_VALUE è una percentuale, non un valore letterale. La query PolyBase avrà esito negativo se la *percentuale* di righe non eseguite supera il valore *reject_value*. La percentuale di righe con esito negativo viene calcolata a intervalli.  
  
 REJECT_VALUE = *reject_value*  
 Specifica il valore o la percentuale di righe che possono essere rifiutate prima che la query abbia esito negativo.  
  
 Per REJECT_TYPE = value, *reject_value* deve essere un numero intero compreso tra 0 e 2.147.483.647.  
  
 Per REJECT_TYPE = percentage, *reject_value* deve essere un valore float compreso tra 0 e 100.  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 Questo attributo è obbligatorio quando si specifica REJECT_TYPE = percentage. Determina il numero di righe che si deve tentare di recuperare prima che PolyBase ricalcoli la percentuale di righe rifiutate.  
  
 Il parametro *reject_sample_value* deve essere un numero intero compreso tra 0 e 2.147.483.647.  
  
 Ad esempio, se REJECT_SAMPLE_VALUE = 1000, PolyBase calcola la percentuale di righe con esito negativo dopo che ha tentato di importare 1000 righe dal file di dati esterno. Se la percentuale di righe con esito negativo è inferiore al valore *reject_value*, PolyBase tenterà di recuperare altre 1000 righe. Continua a ricalcolare la percentuale di righe con esito negativo dopo aver tentato di importare ognuna delle 1000 righe aggiuntive.  
  
> [!NOTE]  
>  Poiché PolyBase calcola la percentuale di righe con esito negativo a intervalli, la percentuale effettiva di tali righe può superare *reject_value*.  
  

Esempio:  
  
 Questo esempio illustra come le tre opzioni REJECT interagiscono tra loro. Ad esempio, se REJECT_TYPE = percentage, REJECT_VALUE = 30 e REJECT_SAMPLE_VALUE = 100, potrebbe verificarsi il seguente scenario:  
  
-   PolyBase tenta di recuperare le prime 100 righe di cui 25 avranno esito negativo e 75 esito positivo.  
  
-   La percentuale di righe con esito negativo viene calcolata come 25%, che è minore del valore di rifiuto pari al 30%. Di conseguenza, PolyBase continuerà a recuperare i dati dall'origine dati esterna.  
  
-   PolyBase tenta di caricare le 100 righe successive: questa volta 25 hanno esito positivo e 75 esito negativo.  
  
-   Percentuale di righe con esito negativo viene ricalcolata come 50%. La percentuale di righe con esito negativo ha superato il valore di rifiuto del 30%.  
  
-   La query PolyBase ha esito negativo con il 50% di righe rifiutate dopo aver tentato di restituire le prime 200 righe. Si noti che le righe corrispondenti vengono restituite prima che la query PolyBase rilevi che è stata superata la soglia di rifiuto.  
  
REJECTED_ROW_LOCATION = *posizione della directory*
  
  Specifica la directory all'interno dell'origine dati esterna in cui vengono scritte le righe rifiutate e il file di errori corrispondente.
Se il percorso specificato non esiste, PolyBase ne crea uno automaticamente. Viene creata una directory figlio con nome "_rejectedrows". Il carattere "_" assicura che la directory venga ignorata da altre attività di elaborazione dati, salvo se indicata in modo esplicito nel parametro del percorso. Questa directory include una cartella creata in base all'ora di inoltro del carico, con il formato AnnoMeseGiorno - OraMinutoSecondo (ad esempio 20180330-173205). In questa cartella vengono scritte due tipi di file, i file _reason (file del motivo) e i file di dati. 

Sia i file del motivo che i file di dati hanno il queryID associato all'istruzione CTAS. Poiché i dati e il motivo si trovano in file distinti, i file corrispondenti hanno un suffisso corrispondente. 
  
 Opzioni per la tabella esterna partizionata  
 Specifica l'origine dati esterna (un'origine dati non SQL Server) e un metodo di distribuzione per la [query di database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/).  
  
 DATA_SOURCE  
 Un'origine dati esterna, ad esempio i dati archiviati in un file system Hadoop, un'archiviazione BLOB di Azure o un [gestore di mappe partizioni](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/).  
  
 SCHEMA_NAME  
 La clausola SCHEMA_NAME offre la possibilità di eseguire il mapping della definizione di tabella esterna in una tabella in un altro schema nel database remoto. Usarla per evitare ambiguità tra gli schemi che esistono sia nei database locali che in quelli remoti.  
  
 OBJECT_NAME  
 La clausola OBJECT_NAME offre la possibilità di eseguire il mapping della definizione di tabella esterna in una tabella con un altro nome nel database remoto. Usarla per evitare ambiguità tra i nomi di oggetti che esistono sia nei database locali che in quelli remoti.  
  
 DISTRIBUTION  
 Facoltativo. Richiesta solo per i database di tipo SHARD_MAP_MANAGER. Verifica se una tabella viene trattata come una tabella partizionata o una tabella replicata. Con **SHARDED** (*column_name*) le tabelle sono partizionate e i dati provenienti da tabelle diverse non si sovrappongono. **REPLICATED** specifica che le tabelle devono avere gli stessi dati in ogni partizione. **ROUND_ROBIN** indica che viene usato un metodo specifico di un'applicazione per distribuire i dati.  
  
## <a name="permissions"></a>Permissions  
 Richiede queste autorizzazioni utente:  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 Si noti che l'account di accesso che crea l'origine dati esterna deve avere le autorizzazioni necessarie per leggere e scrivere nell'origine dati esterna, che si trova in Hadoop o nell'archiviazione BLOB di Azure.  


 > [!IMPORTANT]  

>  L'autorizzazione ALTER ANY EXTERNAL DATA SOURCE concede a qualsiasi entità di sicurezza la possibilità di creare e modificare qualsiasi oggetto origine dati esterna e, di conseguenza, la possibilità di accedere a tutte le credenziali con ambito database per il database. Questa autorizzazione deve essere considerata con privilegi elevati e quindi essere concessa solo a entità attendibili nel sistema.

## <a name="error-handling"></a>Gestione degli errori  
 Durante l'esecuzione dell'istruzione CREATE EXTERNAL TABLE, PolyBase tenta di connettersi all'origine dati esterna. Se il tentativo di connessione non riesce, l'istruzione ha esito negativo e la tabella esterna non viene creata. La conferma dell'esito negativo del comando può richiedere almeno un minuto perché PolyBase ritenta la connessione prima di stabilire che la query non riesce.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Negli scenari di query ad hoc, ad esempio SELECT FROM EXTERNAL TABLE, PolyBase archivia le righe recuperate dall'origine dati esterna in una tabella temporanea. Dopo il completamento della query, PolyBase rimuove ed elimina la tabella temporanea. Nessun dato permanente viene archiviato nelle tabelle SQL.  
  
 Al contrario, nello scenario di importazione, ad esempio SELECT INTO FROM EXTERNAL TABLE, PolyBase archivia le righe recuperate dall'origine dati esterna come dati permanenti nella tabella SQL. La nuova tabella viene creata durante l'esecuzione della query quando PolyBase recupera i dati esterni.  
  
 PolyBase può eseguire il push di parte del calcolo della query in Hadoop per migliorare le prestazioni della query. Questa operazione è detta distribuzione del predicato. Per abilitarla, specificare l'opzione del percorso della gestione risorse di Hadoop in [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 È possibile creare numerose tabelle esterne che fanno riferimento alle stesse o ad altre origini dati esterne.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 In CTP2 la funzionalità di esportazione non è supportata, quindi i dati SQL vengono archiviati in modo permanente nell'origine dati esterna. Questa funzionalità sarà disponibile in CTP3.  
  
 Poiché i dati per una tabella esterna risiedono fuori dal dispositivo, non sono sotto il controllo di PolyBase e possono essere modificati o rimossi in qualsiasi momento da un processo esterno. Per questo motivo, non si garantisce che i risultati delle query rispetto a una tabella esterna siano deterministici. La stessa query può restituire risultati diversi ogni volta che viene eseguita su una tabella esterna. Analogamente, una query può non riuscire se i dati esterni vengono rimossi o spostati.  
  
 È possibile creare più tabelle esterne che fanno tutte riferimento a origini dati esterne differenti. Tuttavia, se si eseguono contemporaneamente query su diverse origini dati Hadoop, ogni origine Hadoop deve usare la stessa impostazione di configurazione server "hadoop connectivity". Ad esempio, non è possibile eseguire contemporaneamente una query su un cluster Cloudera Hadoop e un cluster Hortonworks Hadoop poiché usano impostazioni di configurazione diverse. Per le impostazioni di configurazione e le combinazioni supportate, vedere [Configurazione della connettività di PolyBase &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 Solo queste istruzioni Data Definition Language (DDL) sono consentite per le tabelle esterne:  
  
-   CREATE TABLE e DROP TABLE  
  
-   CREATE STATISTICS e DROP STATISTICS  
Nota: CREATE e DROP STATISTICS per le tabelle esterne non sono supportate nel database SQL di Azure. 
  
-   CREATE VIEW e DROP VIEW  
  
 Costrutti e operazioni non supportati:  
  
-   Il vincolo DEFAULT per le colonne di tabelle esterne  
  
-   Operazioni di eliminazione, inserimento e aggiornamento di Data Manipulation Language (DML)  
  
 Limitazioni delle query:  
  
 PolyBase può utilizzare al massimo 33.000 file per cartella durante l'esecuzione di 32 query PolyBase simultanee. Questo numero massimo include i file e le sottocartelle presenti in ogni cartella HDFS. Se il livello di concorrenza è inferiore a 32, un utente può eseguire le query PolyBase sulle cartelle in HDFS che contengono più di 33.000 file. È consigliabile usare percorsi brevi per i file esterni e non più di 30.000 file per ogni cartella HDFS. Quando si fa riferimento a troppi file, potrebbe verificarsi un'eccezione di memoria insufficiente in Java Virtual Machine (JVM).  

Limitazioni della larghezza della tabella: PolyBase in SQL Server 2016 ha un limite di larghezza di riga di 32 KB, in base alla dimensione massima di una singola riga valida secondo la definizione della tabella. Se la somma dello schema di colonne è maggiore di 32 KB, PolyBase non sarà in grado di eseguire query sui dati. 

In SQL Data Warehouse questa limitazione è stata aumentata a 1 MB.


## <a name="locking"></a>Utilizzo di blocchi  
 Blocco condiviso per l'oggetto SCHEMARESOLUTION.  
  
## <a name="security"></a>Security  
 I file di dati per una tabella esterna viene archiviato in Hadoop o nell'archiviazione BLOB di Azure. Questi file di dati vengono creati e gestiti dai processi dell'utente, che sarà responsabile della gestione della sicurezza dei dati esterni.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. Creare una tabella esterna con dati in formato di testo delimitato.  
 Questo esempio illustra tutti i passaggi necessari per creare una tabella esterna i cui dati sono formattati in file di testo delimitato. Definisce un'origine dati esterna *mydatasource* e un formato di file esterno *myfileformat*. A questi oggetti a livello di database viene fatto riferimento nell'istruzione CREATE EXTERNAL TABLE. Per altre informazioni, vedere [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. Creare una tabella esterna con dati in formato RCFILE.  
 Questo esempio illustra tutti i passaggi necessari per creare una tabella esterna i cui dati sono formattati come RCFILE. Definisce un'origine dati esterna *mydatasource_rc* e un formato di file esterno *myfileformat_rc*. A questi oggetti a livello di database viene fatto riferimento nell'istruzione CREATE EXTERNAL TABLE. Per altre informazioni, vedere [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. Creare una tabella esterna con dati in formato ORC.  
 Questo esempio illustra tutti i passaggi necessari per creare una tabella esterna i cui dati sono formattati come file ORC. Definisce un'origine dati esterna mydatasource_orc e un formato di file esterno myfileformat_orc. A questi oggetti a livello di database viene fatto riferimento nell'istruzione CREATE EXTERNAL TABLE. Per altre informazioni, vedere [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md) e [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. Eseguire query sui dati Hadoop  
 Clickstream è una tabella esterna che si connette al file di testo delimitato employee.tbl in un cluster Hadoop. La query seguente è simile a una query eseguita su una tabella standard. Tuttavia, questa query recupera i dati da Hadoop e quindi calcola i risultati.  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. Unire i dati Hadoop con i dati SQL  
 Questa query è simile a un JOIN standard in due tabelle SQL. La differenza è che PolyBase recupera i dati Clickstream da Hadoop e li aggiunge alla tabella UrlDescription. Una tabella è una tabella esterna e l'altra è una tabella SQL standard.  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. Importare dati da Hadoop in una tabella SQL  
 In questo esempio viene creata una nuova tabella SQL ms_user che archivia in modo permanente il risultato di un join tra la tabella SQL standard *user* e la tabella esterna *ClickStream*.  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. Creare una tabella esterna per un'origine dati partizionata  
 In questo esempio viene rieseguito il mapping di una DMV remota a una tabella esterna usando le clausole SCHEMA_NAME e OBJECT_NAME.  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. Importazione di dati da ADLS in Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH
(
    FORMAT_TYPE = DELIMITEDTEXT 
    , FORMAT_OPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
)


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH
(
    LOCATION='/DimProduct/' , 
    DATA_SOURCE = AzureDataLakeStore , 
    FILE_FORMAT = TextFileFormat , 
    REJECT_TYPE = VALUE ,
    REJECT_VALUE = 0
) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. Unire le tabelle esterne  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. Unire i dati HDFS con i dati PDW  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. Importare i dati delle righe da HDFS in una tabella PDW distribuita  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. Importare i dati delle righe da HDFS in una tabella PDW replicata  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di query di metadati comuni (SQL Server PDW)](https://msdn.microsoft.com/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



