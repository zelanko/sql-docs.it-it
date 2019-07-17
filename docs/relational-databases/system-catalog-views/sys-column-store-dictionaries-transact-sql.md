---
title: Sys. column_store_dictionaries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f675e4d0d40bf9e1db4bf2de6b66b1acfc039873
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140017"
---
# <a name="syscolumnstoredictionaries-transact-sql"></a>sys.column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni dizionario utilizzato negli indici columnstore con ottimizzazione per la memoria xVelocity. I dizionari vengono utilizzati per codificare alcuni tipi di dati, ma non tutti. Pertanto non tutte le colonne in un indice columnstore contengono dizionari. Un dizionario può essere presente come dizionario primario (per tutti i segmenti) e possibilmente per altri dizionari secondari utilizzati per un subset di segmenti della colonna.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|ID dell'heap o dell'indice ad albero B (HoBT) per la tabella a cui appartiene l'indice columnstore.|  
|**column_id**|**int**|ID della colonna columnstore inizia con 1. La prima colonna con ID = 1, la seconda colonna con ID = 2, e così via.|  
|**dictionary_id**|**int**|Possono essere presenti due tipi di dizionari, globali e locali, associati a un segmento di colonna. Un dictionary_id pari a 0 rappresenta il dizionario globale condiviso tra tutti i segmenti di colonna (uno per ogni gruppo di righe) per tale colonna.|  
|**version**|**int**|Versione del formato del dizionario.|  
|**type**|**int**|Tipo di dizionario:<br /><br /> 1 - hash dizionario contenente **int** valori<br /><br /> 2 - non utilizzato<br /><br /> 3 - dizionario di hash contenente valori stringa<br /><br /> 4 - hash dizionario contenente **float** valori<br /><br /> Per altre informazioni sui dizionari, vedere [Guida agli indici Columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md).|  
|**last_id**|**int**|L'ultimo ID dati nel dizionario.|  
|**entry_count**|**bigint**|Numero di voci nel dizionario.|  
|**on_disc_size**|**bigint**|Dimensioni del dizionario in byte.|  
|**partition_id**|**bigint**|Indica l'ID della partizione. Valore univoco all'interno di un database.|  
  
## <a name="permissions"></a>Permissions  
 Tutte le colonne richiedono almeno l'autorizzazione VIEW DEFINITION sulla tabella. Le colonne seguenti restituiscono null a meno che l'utente ha inoltre **seleziona** autorizzazione: last_id, entry_count, data_ptr.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [L'esecuzione di query nel catalogo di sistema SQL Server domande frequenti](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

