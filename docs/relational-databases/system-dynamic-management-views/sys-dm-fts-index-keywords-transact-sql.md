---
title: sys.dm_fts_index_keywords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords
- sys.dm_fts_index_keywords
- sys.dm_fts_index_keywords_TSQL
- dm_fts_index_keywords_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords dynamic management function
- full-text search [SQL Server], viewing keywords
- troubleshooting [SQL Server], full-text search
ms.assetid: fce7b2a1-7e74-4769-86a8-c77c7628decd
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: de956e2dffebd801205bf4ac46a7f503e1acbe8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944281"
---
# <a name="sysdmftsindexkeywords-transact-sql"></a>sys.dm_fts_index_keywords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sul contenuto di un indice full-text per la tabella specificata.  
  
 **DM fts_index_keywords** è una funzione a gestione dinamica.  
  
> [!NOTE]  
>  Per visualizzare le informazioni sugli indici full-text di livello inferiore, usare il [DM fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md) funzione a gestione dinamica a livello di documento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.dm_fts_index_keywords( DB_ID('database_name'), OBJECT_ID('table_name') )  
```  
  
## <a name="arguments"></a>Argomenti  
 db_id('*database_name*')  
 Una chiamata per il [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) (funzione). Questa funzione accetta un nome di database e restituisce l'ID del database, quale **DM fts_index_keywords** Usa per individuare il database specificato. Se *database_name* viene omesso, viene restituito l'ID del database corrente.  
  
 object_id('*table_name*')  
 Una chiamata per il [object_id ()](../../t-sql/functions/object-id-transact-sql.md) (funzione). Tale funzione accetta un nome di tabella e restituisce l'ID della tabella che contiene l'indice full-text da controllare.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**keyword**|**nvarchar(4000)**|Rappresentazione esadecimale della parola chiave archiviata nell'indice full-text.<br /><br /> Nota: OxFF rappresenta il carattere speciale che indica la fine di un file o set di dati.|  
|**display_term**|**nvarchar(4000)**|Formato leggibile della parola chiave derivato dal formato esadecimale.<br /><br /> Nota: Il **display_term** valore per OxFF è "END OF FILE".|  
|**column_id**|**int**|ID della colonna utilizzata per eseguire l'indicizzazione full-text della parola chiave corrente.|  
|**document_count**|**int**|Numero di documenti o righe che contengono il termine corrente.|  
  
## <a name="remarks"></a>Note  
 Le informazioni restituite da **DM fts_index_keywords** sono utili per individuare le operazioni seguenti, tra le altre cose:  
  
-   Appartenenza di una parola chiave all'indice full-text.  
  
-   Numero di documenti o righe che contengono una parola chiave specificata.  
  
-   Parola chiave più comune nell'indice full-text:  
  
    -   **document_count** della ognuno *keyword_value* rispetto al totale **document_count**, il numero di documenti di 0xFF.  
  
    -   In genere è più appropriato definire come parole non significative le parole chiave più comuni.  
  
> [!NOTE]  
>  Il **document_count** restituito da **DM fts_index_keywords** può essere meno preciso per un documento specifico rispetto al conteggio restituito da **DM fts_index_keywords_by_document** o un **CONTAINS** query. Questa possibile imprecisione è stimata essere minore dell'1%. Questo può verificarsi in quanto un **document_id** potrebbero essere conteggiati due volte se si ripete in più di una riga nel frammento di indice, o se viene visualizzato più volte nella stessa riga. Per ottenere un conteggio più preciso per un documento specifico, usare **DM fts_index_keywords_by_document** o una **CONTAINS** query.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-high-level-full-text-index-content"></a>A. Visualizzazione del contenuto dell'indice full-text di alto livello  
 Nell'esempio seguente vengono visualizzate informazioni sul contenuto di alto livello dell'indice full-text nella tabella `HumanResources.JobCandidate`.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords(db_id('AdventureWorks2012'), object_id('HumanResources.JobCandidate'))  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica la ricerca semantica e ricerca full-Text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Ricerca full-text](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
