---
title: sys.dm_exec_describe_first_result_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set
- sys.dm_exec_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set catalog view
ms.assetid: 6ea88346-0bdb-4f0e-9f1f-4d85e3487d23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 72244883d45245efcdcbcf8aba9e4db4c6e25a8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013436"
---
# <a name="sysdmexecdescribefirstresultset-transact-sql"></a>sys.dm_exec_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Questa funzione a gestione dinamica accetta un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione come parametro e descrive i metadati del primo set di risultati per l'istruzione.  
  
 **DM exec_describe_first_result_set** dispone di definizione del set dello stesso risultato [DM exec_describe_first_result_set_for_object &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md) ed è simile al [sp _ describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  

 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.dm_exec_describe_first_result_set(@tsql, @params, @include_browse_information)  
```  
  
## <a name="arguments"></a>Argomenti  
 *\@tsql*  
 Una o più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. *SQL_batch Transact* può essere **nvarchar (***n***)** oppure **nvarchar (max)**.  
  
 *\@params*  
 \@params fornisce una stringa di dichiarazione per i parametri per il [!INCLUDE[tsql](../../includes/tsql-md.md)] batch, simile a sp_executesql. I parametri possono essere **nvarchar (n)** oppure **nvarchar (max)**.  
  
 Stringa che contiene le definizioni di tutti i parametri che sono stati incorporati nel [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*. La stringa deve essere una costante o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n* è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato in stmt deve essere definito \@params. Se il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch nell'istruzione non contiene parametri, \@params non è obbligatorio. Il valore predefinito per questo parametro è NULL.  
  
 *\@include_browse_information*  
 Se impostato su 1, ogni query viene analizzata come se per essa fosse stata specificata un'opzione FOR BROWSE. Vengono restituite informazioni aggiuntive sulla tabella di origine e sulle colonne chiave.  
  
## <a name="table-returned"></a>Tabella restituita  
 Questi metadati comuni vengono restituiti come un set di risultati. In una riga di ogni colonna nei metadati dei risultati viene fornita la descrizione del tipo e l'ammissione di valori Null della colonna nel formato illustrato nella tabella seguente. Se la prima istruzione non esiste per ogni percorso di controllo, viene restituito un set di risultati con zero righe.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|Specifica che la colonna è una colonna aggiuntiva inserita a scopo informativo e di esplorazione che non compare effettivamente nel set di risultati.|  
|**column_ordinal**|**int**|Contiene la posizione ordinale della colonna nel set di risultati. La posizione della prima colonna viene specificata come 1.|  
|**name**|**sysname**|Contiene il nome della colonna se è possibile determinare un nome. In caso contrario, conterrà NULL.|  
|**is_nullable**|**bit**|Contiene i valori seguenti:<br /><br /> Valore 1 se la colonna ammette valori NULL.<br /><br /> Valore 0 se la colonna non ammette valori NULL.<br /><br /> Valore 1 se non è possibile determinare se la colonna ammette valori NULL.|  
|**system_type_id**|**int**|Contiene il system_type_id del tipo di dati della colonna come specificato in sys. Types. Per i tipi CLR, anche se la colonna system_type_name restituisce NULL, in questa colonna viene restituito il valore 240.|  
|**system_type_name**|**nvarchar(256)**|Contiene il nome e gli argomenti, ad esempio lunghezza, precisione e scala, specificati per il tipo di dati della colonna.<br /><br /> Se il tipo di dati è un tipo di alias definito dall'utente, il tipo di sistema sottostante viene specificato qui.<br /><br /> Se il tipo di dati è un tipo CLR definito dall'utente, in questa colonna viene restituito NULL.|  
|**max_length**|**smallint**|Lunghezza massima in byte della colonna.<br /><br /> -1 = il tipo di dati della colonna **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, oppure **xml**.<br /><br /> Per la **testo** colonne, il **max_length** valore sarà 16 o il valore impostato dal **sp_tableoption 'text in row'**.|  
|**precisione**|**tinyint**|Precisione della colonna se basata su valori numerici. In caso contrario, restituisce 0.|  
|**scala**|**tinyint**|Scala della colonna se basata su valori numerici. In caso contrario, restituisce 0.|  
|**nome_regole_di_confronto**|**sysname**|Nome delle regole di confronto della colonna se basata su caratteri. In caso contrario, viene restituito NULL.|  
|**user_type_id**|**int**|Per i tipi di alias e CLR, contiene il valore user_type_id del tipo di dati della colonna come specificato in sys.types. In caso contrario, è NULL.|  
|**user_type_database**|**sysname**|Per i tipi di alias e CLR, contiene il nome del database in cui è definito il tipo. In caso contrario, è NULL.|  
|**user_type_schema**|**sysname**|Per i tipi di alias e CLR, contiene il nome dello schema in cui è definito il tipo. In caso contrario, è NULL.|  
|**user_type_name**|**sysname**|Per i tipi di alias e CLR, contiene il nome del tipo. In caso contrario, è NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Per i tipi CLR, restituisce il nome dell'assembly e la classe che definisce il tipo. In caso contrario, è NULL.|  
|**xml_collection_id**|**int**|Contiene il valore xml_collection_id del tipo di dati della colonna come specificato in sys.columns. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_database**|**sysname**|Contiene il database in cui viene definita la raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_schema**|**sysname**|Contiene lo schema in cui viene definita la raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**xml_collection_name**|**sysname**|Contiene il nome della raccolta XML Schema associata a questo tipo. Questa colonna restituisce NULL se il tipo restituito non è associato a una raccolta XML Schema.|  
|**is_xml_document**|**bit**|Restituisce 1 se il tipo di dati restituito è XML ed è garantito che questo tipo sia un documento XML completo (incluso un nodo radice), contrariamente a un frammento XML. In caso contrario, restituisce 0.|  
|**is_case_sensitive**|**bit**|Restituisce 1 se la colonna è di un tipo stringa con distinzione tra maiuscole e minuscole. In caso contrario, restituisce 0.|  
|**is_fixed_length_clr_type**|**bit**|Restituisce 1 se la colonna è di un tipo CLR a lunghezza fissa. In caso contrario, restituisce 0.|  
|**source_server**|**sysname**|Nome del server di origine (se ha origine in un server remoto). Il nome è specificato come viene visualizzato in sys. Servers. Restituisce NULL se la colonna ha origine nel server locale o se non è possibile determinare in quale server ha origine. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_database**|**sysname**|Nome del database di origine restituito dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare il database. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_schema**|**sysname**|Nome dello schema di origine restituito dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare lo schema. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_table**|**sysname**|Nome della tabella di origine restituita dalla colonna in questo risultato. Restituisce NULL se non è possibile determinare la tabella. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**source_column**|**sysname**|Nome della colonna di origine restituita dalla colonna del risultato. Restituisce NULL se non è possibile determinare la colonna. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**is_identity_column**|**bit**|Restituisce 1 se la colonna è una colonna Identity e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna è una colonna Identity.|  
|**is_part_of_unique_key**|**bit**|Restituisce 1 se la colonna fa parte di un indice univoco, inclusi vincoli univoci e primari, e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna fa parte di un indice univoco. Viene popolata solo se sono richieste informazioni di esplorazione.|  
|**is_updateable**|**bit**|Restituisce 1 se la colonna può essere aggiornata e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna può essere aggiornata.|  
|**is_computed_column**|**bit**|Restituisce 1 se la colonna è una colonna calcolata e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna è una colonna calcolata.|  
|**is_sparse_column_set**|**bit**|Restituisce 1 se la colonna è una colonna di tipo sparse e 0 in caso contrario. Restituisce NULL se non è possibile determinare se la colonna fa parte di un set di colonne di tipo sparse.|  
|**ordinal_in_order_by_list**|**smallint**|La posizione della colonna è nell'elenco ORDER BY. Restituisce NULL se la colonna non compare nell'elenco ORDER BY o se l'elenco ORDER BY non può essere determinato in modo univoco.|  
|**order_by_list_length**|**smallint**|Lunghezza dell'elenco ORDER BY. Restituisce NULL se non è presente alcun elenco ORDER BY o se l'elenco ORDER BY non può essere determinato in modo univoco. Si noti che questo valore sarà lo stesso per tutte le righe restituite da sp_describe_first_result_set.|  
|**order_by_is_descending**|**smallint NULL**|Se ordinal_in_order_by_list non è NULL, il **order_by_is_descending** colonna indica la direzione della clausola ORDER BY per questa colonna. In caso contrario, viene restituito NULL.|  
|**error_number**|**int**|Contiene il numero dell'errore restituito dalla funzione. La colonna contiene NULL se non si è verificato alcun errore.|  
|**error_severity**|**int**|Contiene la gravità restituita dalla funzione. La colonna contiene NULL se non si è verificato alcun errore.|  
|**error_state**|**int**|Contiene il messaggio di stato restituito dalla funzione. La colonna contiene NULL se non si è verificato alcun errore.|  
|**error_message**|**nvarchar(4096)**|Contiene il messaggio restituito dalla funzione. La colonna contiene NULL se non si è verificato alcun errore.|  
|**error_type**|**int**|Contiene un numero intero che rappresenta l'errore restituito. Viene eseguito il mapping a error_type_desc. Vedere l'elenco nelle osservazioni.|  
|**error_type_desc**|**nvarchar(60)**|Contiene una breve stringa in caratteri maiuscoli che rappresenta l'errore restituito. Viene eseguito il mapping a error_type. Vedere l'elenco nelle osservazioni.|  
  
## <a name="remarks"></a>Note  
 Questa funzione utilizza lo stesso algoritmo **sp_describe_first_result_set**. Per altre informazioni, vedere [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
 Nella tabella seguente vengono elencati i tipi di errore con le relative descrizioni  
  
|error_type|error_type|Descrizione|  
|-----------------|-----------------|-----------------|  
|1|MISC|Tutti gli errori che non sono stati descritti.|  
|2|SYNTAX|Errore di sintassi nel batch.|  
|3|CONFLICTING_RESULTS|Impossibile determinare il risultato a causa di un conflitto tra due possibili prime istruzioni.|  
|4|DYNAMIC_SQL|Impossibile determinare il risultato perché codice SQL dinamico potrebbe potenzialmente restituire il primo risultato.|  
|5|CLR_PROCEDURE|Impossibile determinare il risultato perché una stored procedure CLR potrebbe potenzialmente restituire il primo risultato.|  
|6|CLR_TRIGGER|Impossibile determinare il risultato perché un trigger CLR potrebbe potenzialmente restituire il primo risultato.|  
|7|EXTENDED_PROCEDURE|Impossibile determinare il risultato perché una stored procedure estesa potrebbe potenzialmente restituire il primo risultato.|  
|8|UNDECLARED_PARAMETER|Non è stato possibile determinare il risultato perché il tipo di dati di uno o più colonne del set di risultati dipende potenzialmente da un parametro non dichiarato.|  
|9|RECURSION|Non è stato possibile determinare il risultato perché il batch contiene un'istruzione ricorsiva.|  
|10|TEMPORARY_TABLE|Non è stato possibile determinare il risultato perché il batch contiene una tabella temporanea e non è supportato dal **sp_describe_first_result_set** .|  
|11|UNSUPPORTED_STATEMENT|Non è stato possibile determinare il risultato perché il batch contiene un'istruzione che non è supportata dal **sp_describe_first_result_set** (ad esempio FETCH, REVERT e così via.).|  
|12|OBJECT_TYPE_NOT_SUPPORTED|Il \@object_id passato alla funzione non è supportato (vale a dire non una stored procedure)|  
|13|OBJECT_DOES_NOT_EXIST|Il \@object_id passato alla funzione non è stato trovato nel catalogo di sistema.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione per eseguire il \@argomento tsql.  
  
## <a name="examples"></a>Esempi  
 Esempi aggiuntivi nell'argomento [sp_describe_first_result_set &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) possono essere adattati per l'uso **DM exec_describe_first_result_set**.  
  
### <a name="a-returning-information-about-a-single-transact-sql-statement"></a>A. Restituzione di informazioni su una sola istruzione Transact-SQL  
 Nel codice seguente vengono restituite informazioni sui risultati di un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_exec_describe_first_result_set  
(N'SELECT object_id, name, type_desc FROM sys.indexes', null, 0) ;  
```  
  
### <a name="b-returning-information-about-a-procedure"></a>B. Restituzione di informazioni su una procedura  
 L'esempio seguente crea una stored procedure denominata pr_TestProc che restituisce due set di risultati. Nell'esempio viene dimostrato che **DM exec_describe_first_result_set** restituisce informazioni sul primo set nella procedura di risultati.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE PROC Production.TestProc  
AS  
SELECT Name, ProductID, Color FROM Production.Product ;  
SELECT Name, SafetyStockLevel, SellStartDate FROM Production.Product ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set  
('Production.TestProc', NULL, 0) ;  
```  
  
### <a name="c-returning-metadata-from-a-batch-that-contains-multiple-statements"></a>C. Restituzione di metadati da un batch che contiene più istruzioni  
 Nell'esempio seguente viene valutato un batch che contiene due istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il set di risultati descrive il primo set di risultati restituito.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set(  
N'SELECT CustomerID, TerritoryID, AccountNumber FROM Sales.Customer WHERE CustomerID = @CustomerID;  
SELECT * FROM Sales.SalesOrderHeader;',  
N'@CustomerID int', 0) AS a;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
