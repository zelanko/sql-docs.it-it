---
title: suspect_pages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70dffcbf2ac3eac13f7ef42e901c4fcd99dce769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130545"
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni pagina che non è riuscita con un errore 823 secondario o un errore 824. Le pagine sono elencate in questa tabella perché è possibile che siano errate. Quando una pagina sospetta viene ripristinata, il relativo stato viene aggiornato nel **event_type** colonna.  
  
 La tabella seguente, che ha un limite di 1.000 righe, viene archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID del database al quale è associata la pagina corrente.|  
|**file_id**|**int**|ID del file nel database.|  
|**page_id**|**bigint**|ID della pagina sospetta. Ogni pagina possiede un ID, rappresentato da un valore a 32 bit, che ne identifica la posizione all'interno del database. Il **page_id** è l'offset nel file di dati della pagina da 8 KB. Ogni ID di pagina è univoco in un file.|  
|**event_type**|**int**|Tipo di errore. I tipi possibili sono:<br /><br /> 1 = errore 823 che indica una pagina sospetta (ad esempio, un errore del disco) o errore 824 diverso da un checksum errato o una pagina incompleta (ad esempio, un ID di pagina errato).<br /><br /> 2 = checksum errato.<br /><br /> 3 = pagina incompleta.<br /><br /> 4 = ripristinata (la pagina è stata ripristinata dopo essere stata contrassegnata come non corretta).<br /><br /> 5 = corretta (la pagina è stata corretta da DBCC).<br /><br /> 7 = deallocata da DBCC.|  
|**error_count**|**int**|Numero di volte che si è verificato l'errore.|  
|**last_update_date**|**datetime**|Timestamp relativo all'ultimo aggiornamento.|  
  
## <a name="permissions"></a>Permissions  
 Chiunque abbia accesso a **msdb** può leggere i dati nella tabella **suspect_pages** . Chiunque disponga dell'autorizzazione UPDATE nella tabella suspect_pages può aggiornare i relativi record. I membri del ruolo predefinito del database **db_owner** in **msdb** o del ruolo predefinito del server **sysadmin** possono inserire, aggiornare ed eliminare i record.  
  
## <a name="see-also"></a>Vedere anche  
 [Ripristino di pagine &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Classe di evento della pagina di database Suspect Data](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
