---
title: sys.pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 201af9001703bb8f1dfbdaf2c41151697b945df3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059400"
---
# <a name="syspdwnodescolumns-transact-sql"></a>sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Mostra le colonne per le tabelle definite dall'utente e le viste definite dall'utente.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID dell'oggetto a cui appartiene la colonna.||  
|name|**sysname**|Nome della colonna. Deve essere univoco nell'oggetto.||  
|column_id|**int**|ID della colonna. Deve essere univoco nell'oggetto.||  
|system_type_id|**tinyint**|ID del tipo di sistema della colonna.||  
|user_type_id|**int**|ID del tipo di colonna definito dall'utente.||  
|max_length|**smallint**|Lunghezza massima in byte della colonna.|Include -1 (non valido) per i tipi di colonna non supportata.|  
|precisione|**tinyint**|Precisione della colonna se la colonna è di tipo numerico. In caso contrario, 0.||  
|scala|**tinyint**|Scala della colonna se di tipo numerico, altrimenti 0.||  
|collation_name|**sysname**|Nome delle regole di confronto della colonna se la colonna è di tipo carattere. In caso contrario, NULL.||  
|is_nullable|**bit**|1 = La colonna ammette valori Null.||  
|is_ansi_padded|**bit**|1 = La colonna utilizza l'opzione ANSI_PADDING ON se è di tipo carattere, binary o variant.|Sempre 0.|  
|is_rowguidcol|**bit**|1 = La colonna è una parola chiave ROWGUIDCOL dichiarata.|Sempre 0.|  
|is_identity|**bit**|1 = La colonna include valori Identity.|Sempre 0.|  
|is_computed|**bit**|1 = La colonna è una colonna calcolata.|Sempre 0.|  
|is_filestream|**bit**|1 = la colonna è una colonna FILESTREAM.|Sempre 0.|  
|is_replicated|**bit**|1 = La colonna viene replicata.|Sempre 0.|  
|is_non_sql_subscribed|**bit**|1 = colonna è associato un sottoscrittore non SQL.|Sempre 0.|  
|is_merge_published|**bit**|1 = La colonna è inclusa in una pubblicazione di tipo merge.|Sempre 0.|  
|is_dts_replicated|**bit**|1 = colonna viene replicata tramite SSIS.|Sempre 0.|  
|is_xml_document|**bit**|1 = Il contenuto è un documento XML completo.|Sempre 0.|  
|xml_collection_id|**int**|0 = Nessuna raccolta di XML Schema.|Sempre 0.|  
|default_object_id|**int**|ID dell'oggetto predefinito. 0 = nessun valore predefinito.|Sempre 0.|  
|rule_object_id|**int**|ID della regola autonoma associata alla colonna. <br />0 = Nessuna regola autonoma.|Sempre 0.|  
|is_sparse|**bit**|1 = La colonna è di tipo sparse.|Sempre 0.|  
|is_column_set|**bit**|1 = La colonna è un set di colonne.|Sempre 0.|  
|pdw_node_id|**int**|Identificatore univoco di un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL SERVER.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
