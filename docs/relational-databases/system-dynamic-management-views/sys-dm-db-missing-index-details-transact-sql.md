---
title: sys.dm_db_missing_index_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1fc72e290bf1aa495493eb09d5e0db8cf305202e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62508250"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce informazioni dettagliate sugli indici mancanti, escludendo gli indici spaziali.  
  
 In [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], le viste a gestione dinamica non possono esporre le informazioni che influenzerebbero l'indipendenza del database o le informazioni sugli altri database a cui l'utente dispone di accesso. Per evitare di esporre queste informazioni, ogni riga che contiene dati che non appartengono al tenant connesso viene filtrata.  

  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|Identifica un determinato indice mancante. L'identificatore è univoco nel server. **index_handle** è la chiave di questa tabella.|  
|**database_id**|**smallint**|Identifica il database in cui è archiviata la tabella con l'indice mancante.|  
|**object_id**|**int**|Identifica la tabella in cui l'indice risulta mancante.|  
|**equality_columns**|**nvarchar(4000)**|Elenco delimitato da virgole delle colonne che contribuiscono ai predicati di uguaglianza nel formato seguente:<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|Elenco delimitato da virgole delle colonne che contribuiscono ai predicati di disuguaglianza, ad esempio predicati nel formato seguente:<br /><br /> *table.column* > *constant_value*<br /><br /> Qualsiasi operatore di confronto diverso da "=" esprime disuguaglianza.|  
|**included_columns**|**nvarchar(4000)**|Elenco delimitato da virgole delle colonne necessarie come colonne di copertura per la query. Per altre informazioni sulla copertura o le colonne incluse, vedere [creare indici con colonne incluse](../../relational-databases/indexes/create-indexes-with-included-columns.md).<br /><br /> Per gli indici con ottimizzazione per la memoria (sia hash con ottimizzazione per la memoria non cluster), ignorare **included_columns**. Tutte le colonne della tabella vengono incluse in ogni indice ottimizzato per la memoria.|  
|**istruzione**|**nvarchar(4000)**|Nome della tabella in cui l'indice risulta mancante.|  
  
## <a name="remarks"></a>Note  
 Le informazioni restituite da **DM db_missing_index_details** viene aggiornato quando una query ottimizzata da query optimizer e non è persistente. Le informazioni relative agli indici mancanti vengono mantenute solo fino al riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per mantenere tali informazioni anche dopo il riciclo del server, gli amministratori di database devono eseguirne periodicamente copie di backup.  
  
 Per individuare un determinato indice mancante i gruppi di indici mancanti a cui fa parte di, è possibile eseguire una query di **db_missing_index_groups** vista a gestione dinamica appartiene con **DM db_missing_index_details**  base il **index_handle** colonna.  

  >[!NOTE]
  >Set di risultati di questa DMV sono limitato a 600 righe. Ogni riga contiene un indice mancano. Se si dispone di più di 600 degli indici mancanti, è necessario risolvere tutti gli indici mancanti esistenti in modo che è quindi possibile visualizzare quelli più recenti. 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>Utilizzo di informazioni sugli indici mancanti in istruzioni CREATE INDEX  
 Per convertire le informazioni restituite da **DM db_missing_index_details** in un'istruzione CREATE INDEX per gli indici con ottimizzazione per la memoria sia basata su disco, le colonne di uguaglianza devono essere inserite prima delle colonne di disuguaglianza e insieme deve costituire la chiave dell'indice. Aggiungere le colonne incluse all'istruzione CREATE INDEX mediante la clausola INCLUDE. Per determinare un ordine efficiente per le colonne di uguaglianza, ordinarle in base alla selettività a partire dalle colonne più selettive, all'estrema sinistra nell'elenco di colonne.  
  
 Per altre informazioni sugli indici con ottimizzazione per la memoria, vedere [indici per tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  
  
## <a name="transaction-consistency"></a>Consistenza delle transazioni  
 Se in una transazione viene creata o eliminata una tabella, le righe contenenti le informazioni sugli indici mancanti per gli oggetti eliminati vengono rimosse da questo oggetto a gestione dinamica, mantenendo la consistenza delle transazioni.  
  
## <a name="permissions"></a>Permissions

Sul [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], è necessario `VIEW SERVER STATE` autorizzazione.   
Sul [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], è necessario il `VIEW DATABASE STATE` autorizzazione nel database.   

## <a name="see-also"></a>Vedere anche  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
