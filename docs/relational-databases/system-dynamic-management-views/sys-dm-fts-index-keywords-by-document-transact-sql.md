---
title: sys.dm_fts_index_keywords_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed1ebf610eafe5c882b2e19ed70129e0cac432fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944363"
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Restituisce informazioni sul contenuto a livello di documento di un indice full-text associato alla tabella specificata.  
  
 sys.dm_fts_index_keywords_by_document è una funzione a gestione dinamica.  
  
 **Per visualizzare informazioni sull'indice full-text di livello superiore**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **Per visualizzare le informazioni sul contenuto a livello di proprietà correlati a una proprietà di documento**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argomenti  
 db_id('*database_name*')  
 Una chiamata per il [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) (funzione). Tale funzione accetta un nome di database e restituisce l'ID del database utilizzato da sys.dm_fts_index_keywords_by_document per eseguire la ricerca del database specificato. Se *database_name* viene omesso, viene restituito l'ID del database corrente.  
  
 object_id('*table_name*')  
 Una chiamata per il [object_id ()](../../t-sql/functions/object-id-transact-sql.md) (funzione). Tale funzione accetta un nome di tabella e restituisce l'ID della tabella che contiene l'indice full-text da controllare.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|colonna|Tipo di dati|Descrizione|  
|------------|---------------|-----------------|  
|parola chiave|**nvarchar(4000)**|Rappresentazione esadecimale della parola chiave archiviata nell'indice full-text.<br /><br /> Nota: OxFF rappresenta il carattere speciale che indica la fine di un file o set di dati.|  
|display_term|**nvarchar(4000)**|Formato leggibile della parola chiave derivato dal formato interno archiviato nell'indice full-text.<br /><br /> Nota: OxFF rappresenta il carattere speciale che indica la fine di un file o set di dati.|  
|column_id|**int**|ID della colonna utilizzata per eseguire l'indicizzazione full-text della parola chiave corrente.|  
|document_id|**int**|ID della riga o del documento utilizzato per eseguire l'indicizzazione full-text del termine corrente. L'ID corrisponde al valore della chiave full-text della riga o del documento specificato.|  
|occurrence_count|**int**|Numero di occorrenze della parola chiave corrente nel documento o nella riga in cui è indicato da **document_id**. Quando '*search_property_name*' è specificato, numero_occorrenze Visualizza solo il numero di occorrenze della parola chiave corrente nella proprietà di ricerca specificata all'interno del documento o della riga.|  
  
## <a name="remarks"></a>Note  
 Le informazioni restituite da sys.dm_fts_index_keywords_by_document sono utili per individuare, tra gli altri, anche gli elementi seguenti:  
  
-   Numero totale di parole chiave contenute in un indice full-text.  
  
-   Appartenenza di una parola chiave a una riga oppure a un documento specificato.  
  
-   Numero di volte in cui una parola chiave è presente nell'indice full-text intero, ovvero:  
  
     ([Somma](../../t-sql/functions/sum-transact-sql.md)(**numero_occorrenze**) in cui **parola chiave**=*valore_parola chiave* )  
  
-   Numero di volte in cui una parola chiave è presente in una riga oppure in un documento specificato.  
  
-   Numero di parole chiave contenute in una riga oppure in un documento specificato.  
  
 È possibile inoltre utilizzare le informazioni fornite da sys.dm_fts_index_keywords_by_document per recuperare tutte le parole chiave che appartengono a una riga oppure a un documento specificato.  
  
 Quando la colonna chiave full-text è, come consigliato, un tipo di dati integer, viene eseguito il mapping diretto di document_id al valore della chiave full-text nella tabella di base.  
  
 Quando invece la colonna chiave full-text utilizza un tipo di dati diverso da integer, document_id non rappresenta la chiave full-text della tabella di base. In questo caso, per identificare la riga nella tabella di base che viene restituita da dm_fts_index_keywords_by_document, è necessario unire questa vista con i risultati restituiti da [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Prima di poter eseguire il join, è necessario archiviare l'output della stored procedure in una tabella temporanea e unire in join la colonna document_id di dm_fts_index_keywords_by_document alla colonna DocId restituita da questa stored procedure. Si noti che un **timestamp** colonna non può ricevere valori al momento dell'inserimento perché sono generati automaticamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pertanto, il **timestamp** colonna deve essere convertita **varbinary (8)** colonne. Nell'esempio seguente sono illustrati i passaggi per l'operazione. In questo esempio *table_id* è l'ID della tabella *database_name* è il nome del database, e *table_name* è il nome della tabella.  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 Sono necessarie l'autorizzazione SELECT per le colonne analizzate dall'indice full-text e le autorizzazioni CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. Visualizzazione del contenuto dell'indice full-text a livello di documento  
 Nell'esempio seguente viene visualizzato il contenuto dell'indice full-text a livello di documento nella tabella `HumanResources.JobCandidate` del database di esempio `AdventureWorks2012`.  
  
> [!NOTE]  
>  È possibile creare questo indice eseguendo l'esempio fornito per il `HumanResources.JobCandidate` nella tabella [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica la ricerca semantica e ricerca full-Text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [Migliorare le prestazioni degli indici full-text](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
