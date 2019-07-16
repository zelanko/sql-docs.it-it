---
title: sp_describe_first_result_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc58447e9893647dfa73643f14455d715625478e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053056"
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Restituisce i metadati per un set di risultati possibili prima di [!INCLUDE[tsql](../../includes/tsql-md.md)] batch. Restituisce un set di risultati vuoto se il batch non restituisce risultati. Genera un errore se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non riesce a determinare i metadati per la prima query che verrà eseguita mediante l'esecuzione di un'analisi statica. La vista a gestione dinamica [DM exec_describe_first_result_set &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) restituisce le stesse informazioni.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ \@tsql = ] 'Transact-SQL_batch'` Uno o più [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni. *SQL_batch Transact* può essere **nvarchar (***n***)** oppure **nvarchar (max)** .  
  
`[ \@params = ] N'parameters'` \@params fornisce una stringa di dichiarazione per i parametri per il [!INCLUDE[tsql](../../includes/tsql-md.md)] batch, che è simile a sp_executesql. I parametri possono essere **nvarchar (n)** oppure **nvarchar (max)** .  
  
 Stringa che contiene le definizioni di tutti i parametri che sono stati incorporati nel [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*. La stringa deve essere una costante o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n* è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato nell'istruzione deve essere definito \@params. Se il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch nell'istruzione non contiene parametri, \@params non è obbligatorio. Il valore predefinito per questo parametro è NULL.  
  
`[ \@browse_information_mode = ] tinyint` Specifica se vengono restituite informazioni sulla tabella di origine e di colonne chiave aggiuntive. Se impostato su 1, ogni query viene analizzata come se per essa fosse stata specificata un'opzione FOR BROWSE. Vengono restituite informazioni aggiuntive sulla tabella di origine e sulle colonne chiave.  
  
-   Se impostato su 0, non viene restituita alcuna informazione.  
  
-   Se impostato su 1, ogni query viene analizzata come se per essa fosse stata specificata un'opzione FOR BROWSE. Verranno restituiti nomi della tabella di base come informazioni sulla colonna di origine.  
  
-   Se impostato su 2, ogni query viene analizzata come se venisse utilizzata per la preparazione o l'esecuzione di un cursore. Verranno restituiti nomi della vista come informazioni sulla colonna di origine.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **sp_describe_first_result_set** restituisce sempre uno stato pari a zero se l'operazione riesce. Se la procedura genera un errore e la procedura viene chiamata come RPC, lo stato restituito viene popolato dal tipo di errore descritto nella colonna error_type di DM exec_describe_first_result_set. Se la procedura viene chiamata da [!INCLUDE[tsql](../../includes/tsql-md.md)], il valore restituito è sempre zero, anche quando si verifica un errore.  
  
## <a name="result-sets"></a>Set di risultati  
 Questi metadati comuni vengono restituiti come set di risultati con una riga per ogni colonna nei metadati dei risultati. Ogni riga descrive il tipo e l'ammissione di valori Null della colonna nel formato descritto nella sezione seguente. Se la prima istruzione non esiste per ogni percorso di controllo, viene restituito un set di risultati con zero righe.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit non NULL**|Indica che la colonna è una colonna aggiuntiva aggiunta per informazioni di esplorazione che non compare effettivamente nel set di risultati.|  
|**column_ordinal**|**int non NULL**|Contiene la posizione ordinale della colonna nel set di risultati. Posizione della prima colonna viene specificata come 1.|  
|**name**|**sysname NULL**|Contiene il nome della colonna se è possibile determinare un nome. In caso contrario, contiene NULL.|  
|**is_nullable**|**bit non NULL**|Contiene il valore 1 se la colonna ammette valori Null, 0 se la colonna non ammette valori Null e 1 se non è possibile determinare se la colonna ammette valori Null.|  
|**system_type_id**|**int non NULL**|Contiene il system_type_id del tipo di dati della colonna come specificato in sys. Types. Per i tipi CLR, anche se la colonna system_type_name restituisce NULL, in questa colonna viene restituito il valore 240.|  
|**system_type_name**|**nvarchar(256) NULL**|Contiene il nome e gli argomenti, ad esempio lunghezza, precisione e scala, specificati per il tipo di dati della colonna. Se il tipo di dati è un tipo di alias definito dall'utente, il tipo di sistema sottostante viene specificato qui. Se è un tipo CLR definito dall'utente, in questa colonna viene restituito NULL.|  
|**max_length**|**smallint non NULL**|Lunghezza massima in byte della colonna.<br /><br /> -1 = il tipo di dati della colonna **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , oppure **xml**.<br /><br /> Per la **testo** colonne, il **max_length** valore sarà 16 o il valore impostato dal **sp_tableoption 'text in row'** .|  
|**precisione**|**tinyint non NULL**|Precisione della colonna se basata su valori numerici. In caso contrario, restituisce 0.|  
|**scala**|**tinyint non NULL**|Scala della colonna se basata su valori numerici. In caso contrario, restituisce 0.|  
|**nome_regole_di_confronto**|**sysname NULL**|Nome delle regole di confronto della colonna se basata su caratteri. In caso contrario, viene restituito NULL.|  
|**user_type_id**|**int NULL**|Per i tipi di alias e CLR, contiene il valore user_type_id del tipo di dati della colonna come specificato in sys.types. In caso contrario, è NULL.|  
|**user_type_database**|**sysname NULL**|Per i tipi di alias e CLR, contiene il nome del database in cui è definito il tipo. In caso contrario, è NULL.|  
|**user_type_schema**|**sysname NULL**|Per i tipi di alias e CLR, contiene il nome dello schema in cui è definito il tipo. In caso contrario, è NULL.|  
|**user_type_name**|**sysname NULL**|Per i tipi di alias e CLR, contiene il nome del tipo. In caso contrario, è NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Per i tipi CLR, restituisce il nome dell'assembly e la classe che definisce il tipo. In caso contrario, è NULL.|  
|**xml_collection_id**|**int NULL**|Contiene il valore xml_collection_id del tipo di dati della colonna come specificato in sys.columns. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_database**|**sysname NULL**|Contiene il database in cui viene definita la raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_schema**|**sysname NULL**|Contiene lo schema in cui viene definita la raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_name**|**sysname NULL**|Contiene il nome della raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**is_xml_document**|**bit non NULL**|Restituisce 1 se il tipo di dati restituito è XML ed è garantito che questo tipo sia un documento XML completo (incluso un nodo radice), contrariamente a un frammento XML. In caso contrario, restituisce 0.|  
|**is_case_sensitive**|**bit non NULL**|Restituisce 1 se la colonna è di un tipo stringa che fa distinzione tra maiuscole e minuscole e 0 in caso contrario.|  
|**is_fixed_length_clr_type**|**bit non NULL**|Restituisce 1 se la colonna è di un tipo CLR a lunghezza fissa e 0 in caso contrario.|  
|**source_server**|**sysname**|Nome del server di origine restituito dalla colonna in questo risultato (se ha origine in un server remoto). Il nome è specificato come viene visualizzato in sys. Servers. Restituisce NULL se la colonna ha origine nel server locale o se non è possibile determinare in quale server ha origine. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_database**|**sysname**|Nome del database di origine restituito dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare il database. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_schema**|**sysname**|Nome dello schema di origine restituito dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare lo schema. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_table**|**sysname**|Nome della tabella di origine restituita dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare la tabella. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_column**|**sysname**|Nome della colonna di origine restituita dalla colonna del risultato. Restituisce NULL se non è possibile determinare la colonna. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**is_identity_column**|**bit NULL**|Restituisce 1 se la colonna è una colonna Identity e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna è una colonna Identity.|  
|**is_part_of_unique_key**|**bit NULL**|Restituisce 1 se la colonna fa parte di un indice univoco (inclusi vincoli univoci e primari) e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna fa parte di un indice univoco. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**is_updateable**|**bit NULL**|Restituisce 1 se la colonna può essere aggiornata e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna può essere aggiornata.|  
|**is_computed_column**|**bit NULL**|Restituisce 1 se la colonna è una colonna calcolata e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna è una colonna calcolata.|  
|**is_sparse_column_set**|**bit NULL**|Restituisce 1 se la colonna è una colonna di tipo sparse e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna fa parte di un set di colonne di tipo sparse.|  
|**ordinal_in_order_by_list**|**smallint NULL**|Posizione della colonna nell'elenco ORDER BY. Restituisce NULL se la colonna non compare nell'elenco ORDER BY o se l'elenco ORDER BY non può essere determinato in modo univoco.|  
|**order_by_list_length**|**smallint NULL**|Lunghezza dell'elenco ORDER BY. Restituisce NULL se non è presente alcun elenco ORDER BY o se l'elenco ORDER BY non può essere determinato in modo univoco. Si noti che questo valore sarà lo stesso per tutte le righe restituite da **sp_describe_first_result_set.**|  
|**order_by_is_descending**|**smallint NULL**|Se ordinal_in_order_by_list non è NULL, il **order_by_is_descending** colonna indica la direzione della clausola ORDER BY per questa colonna. In caso contrario, viene restituito NULL.|  
|**tds_type_id**|**int non NULL**|Per uso interno.|  
|**tds_length**|**int non NULL**|Per uso interno.|  
|**tds_collation_id**|**int NULL**|Per uso interno.|  
|**tds_collation_sort_id**|**tinyint NULL**|Per uso interno.|  
  
## <a name="remarks"></a>Note  
 **sp_describe_first_result_set** garantisce che se la procedura restituisce i metadati del primo set di risultati per (un ipotetico) batch A e se tale batch (A) viene successivamente eseguita quindi il batch verranno (1) genera un errore in fase di ottimizzazione, (2) Genera un errore di run-time, (3) non restituisce alcun risultato impostati oppure (4) restituisce un primo set di risultati con gli stessi metadati descritti da **sp_describe_first_result_set**.  
  
 Il nome, l'ammissione di valori Null e il tipo di dati possono variare. Se **sp_describe_first_result_set** restituisce un set di risultati vuoto, la garanzia è che l'esecuzione del batch verrà restituito alcun set di risultati.  
  
 Questa garanzia presuppone che non sono presenti modifiche di schema pertinente sul server. Modifiche allo schema rilevanti nel server non includono la creazione di tabelle temporanee o variabili di tabella nel batch A tra il momento in cui **sp_describe_first_result_set** viene chiamato e l'ora in cui il set di risultati viene restituito durante esecuzione, incluse le modifiche dello schema effettuate dal batch B.  
  
 **sp_describe_first_result_set** restituisce un errore nei casi seguenti.  
  
-   Se l'input \@tsql non è valida [!INCLUDE[tsql](../../includes/tsql-md.md)] batch. Validità è determinata tramite l'analisi di [!INCLUDE[tsql](../../includes/tsql-md.md)] batch. Eventuali errori generati dal batch durante l'ottimizzazione della query o durante l'esecuzione non vengono considerati quando si determina se il [!INCLUDE[tsql](../../includes/tsql-md.md)] batch è valido.  
  
-   Se \@params non è NULL e contiene una stringa che non è una stringa di dichiarazione sintatticamente valida per i parametri o se contiene una stringa che dichiara qualsiasi parametro più di una volta.  
  
-   Se l'input [!INCLUDE[tsql](../../includes/tsql-md.md)] batch dichiara una variabile locale con lo stesso nome come un parametro dichiarato in \@params.  
  
-   L'istruzione utilizza una tabella temporanea.  
  
-   La query include la creazione di una tabella permanente sulla quale viene eseguita una query.  
  
 Se tutti gli altri controlli hanno esito positivo, vengono presi in considerazione tutti i possibili percorsi del flusso di controllo nel batch di input. Questo vengono presi in considerazione controllo tutte le istruzioni del flusso (GOTO, IF/ELSE, WHILE e [!INCLUDE[tsql](../../includes/tsql-md.md)] blocchi TRY/CATCH), nonché eventuali procedure dinamiche [!INCLUDE[tsql](../../includes/tsql-md.md)] batch o i trigger richiamati dal batch di input da un'istruzione EXEC, un'istruzione DDL che causa Attivazione di trigger DDL o un'istruzione DML che causa l'attivazione di trigger in una tabella di destinazione o in una tabella in cui è stata modificata a causa di operazione di propagazione in un vincolo di chiave esterna. Qualora siano possibili più percorsi di controllo, a un certo punto si verifica l'arresto di un algoritmo.  
  
 Per ogni percorso del flusso di controllo, la prima istruzione (se presente) che restituisce un set di risultati è determinato dal **sp_describe_first_result_set**.  
  
 Se in un batch vengono trovate più prime istruzioni possibili, i relativi risultati possono variare nel numero di colonne, nel nome della colonna, nell'ammissione di valori Null e nel tipo di dati. La gestione delle differenze viene descritta più dettagliatamente qui di seguito:  
  
-   Se il numero di colonne è diverso, viene generato un errore e non viene restituito alcun risultato.  
  
-   Se il nome della colonna è diverso, il nome della colonna restituito è impostato su NULL.  
  
-   Se l'ammissione di valori NULL è diversa, l'impostazione restituita ammette valori NULL.  
  
-   Se il tipo di dati è diverso, viene generato un errore e non viene restituito alcun risultato se non nei casi seguenti:  
  
    -   **varchar(a)** al **varchar(a')** in cui un ' > un.  
  
    -   **varchar(a)** a **varchar (max)**  
  
    -   **nvarchar(a)** al **nvarchar(a')** in cui un ' > un.  
  
    -   **nvarchar(a)** a **nvarchar (max)**  
  
    -   **varbinary(a)** al **varbinary(a')** in cui un ' > un.  
  
    -   **varbinary(a)** a **varbinary (max)**  
  
 **sp_describe_first_result_set** non supporta la ricorsione indiretta.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione per eseguire il \@argomento tsql.  
  
## <a name="examples"></a>Esempi  
  
### <a name="typical-examples"></a>Esempi tipici  
  
#### <a name="a-simple-example"></a>R. Esempio semplice  
 Nell'esempio seguente viene descritto il set di risultati restituito da una singola query.  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 Nell'esempio seguente viene mostrato il set di risultati restituito da una singola query contenente un parametro.  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. Esempi di modalità browse  
 Nei tre esempi seguenti viene illustrata la differenza principale tra le diverse modalità di informazioni di esplorazione. Nei risultati delle query sono state incluse solo le colonne attinenti.  
  
 Nell'esempio in cui viene utilizzato 0 non viene restituita alcuna informazione.  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 Nell'esempio in cui viene utilizzato 1 vengono restituite informazioni come se nella query fosse stata specificata un'opzione FOR BROWSE.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 Nell'esempio in cui viene utilizzato 2 viene indicata l'esecuzione di un'analisi come se si stesse effettuando la preparazione di un cursore.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>Esempi di problemi  
 Negli esempi seguenti vengono utilizzate due tabelle per tutti gli esempi. Eseguire le istruzioni seguenti per creare tabelle di esempio.  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>Errore perché il numero di colonne è diverso  
 Il numero di colonne nei primi set di risultati possibili è diverso in questo esempio.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>Errore perché i tipi di dati sono diversi  
 I tipi delle colonne sono diversi nei vari primi set di risultati possibili.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 Risultato: Errore, tipi non corrispondenti (**int** VS **smallint**).  
  
#### <a name="column-name-cannot-be-determined"></a>Non è possibile determinare il nome della colonna  
 Le colonne nei primi set di risultati possibili variano nella lunghezza per lo stesso tipo di lunghezza variabile, ammissione di valori NULL e nomi delle colonne:  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 Risultato: \<Nome di colonna sconosciuto > **varchar (20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>Nome della colonna forzato a essere identico tramite aliasing  
 Come in precedenza, ma le colonne hanno lo stesso nome tramite l'aliasing delle colonne.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 Risultato: b **varchar (20) NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>Errore perché non è possibile trovare tipi di colonna corrispondenti  
 I tipi di colonne sono diversi nei vari primi set di risultati possibili.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 Risultato: Errore, tipi non corrispondenti (**varchar (10)** VS **nvarchar(10)** ).  
  
#### <a name="result-set-can-return-an-error"></a>Il set di risultati può restituire un errore  
 Il primo set di risultati è errore o set di risultati.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 Risultato: un **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>Alcuni percorsi di codice non restituiscono risultati  
 Il primo set di risultati è Null o un set di risultati.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 Risultato: un **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>Risultato da SQL dinamico  
 Il primo set di risultati è SQL dinamico individuabile perché si tratta di una stringa letterale.  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 Risultato: un **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>Errore di risultato da SQL dinamico  
 Il primo set di risultati non è definito a causa di SQL dinamico.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 Risultato: Errore. Il risultato non è individuabile a causa di SQL dinamico.  
  
#### <a name="result-set-specified-by-user"></a>Set di risultati specificato dall'utente  
 Il primo set di risultati viene specificato manualmente dall'utente.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 Risultato: Column1 **bigint non NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>Errore causato da un set di risultati ambiguo  
 Questo esempio si presuppone che un altro utente denominato user1 disponga di una tabella denominata t1 nello schema predefinito s1 con colonne (un **int non NULL**).  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 Risultato: Errore. T1 può essere dbo.t1 o s1.t1, ognuno con un numero diverso di colonne.  
  
#### <a name="result-even-with-ambiguous-result-set"></a>Risultato anche con set di risultati ambiguo  
 Utilizzare le stesse ipotesi dell'esempio precedente.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 Risultato: una **int NULL** perché sia dbo.t1.a sia s1.t1.a presentano il tipo **int** e supporto di valori null.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
