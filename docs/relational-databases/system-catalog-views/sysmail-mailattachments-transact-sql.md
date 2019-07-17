---
title: sysmail_attachments (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3bdcea5da463e2501954c4bf96ca58bac216eb58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060199"
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni allegato inviato a Posta elettronica database. Utilizzare questa vista quando si desidera ottenere informazioni sugli allegati di Posta elettronica database. Per esaminare tutti i messaggi di posta elettronica elaborati mediante l'utilizzo di posta elettronica Database [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|Identificatore dell'allegato.|  
|**mailitem_id**|**int**|Identificatore dell'elemento di posta contenente l'allegato.|  
|**filename**|**nvarchar(520)**|Nome di file dell'allegato. Quando **attach_query_result** è 1 e **query_attachment_filename** è NULL, posta elettronica Database crea un nome file arbitrario.|  
|**filesize**|**int**|Dimensioni in byte dell'allegato.|  
|**attachment**|**varbinary(max)**|Contenuto dell'allegato.|  
|**last_mod_date**|**datetime**|Data e ora dell'ultima modifica della riga.|  
|**last_mod_user**|**sysname**|Autore dell'ultima modifica della riga.|  
  
## <a name="remarks"></a>Note  
 Quando si risolvono i problemi relativi a Posta elettronica database, è possibile utilizzare questa vista per visualizzare le proprietà degli allegati.  
  
 Gli allegati archiviati nelle tabelle di sistema possono causare il **msdb** crescita del database. Uso **sysmail_delete_mailitems_sp** eliminare elementi di posta elettronica e gli allegati associati. Per altre informazioni, vedere [creare un processo di SQL Server Agent per archivio messaggi di posta elettronica Database e log eventi](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md).  
  
## <a name="permissions"></a>Permissions  
 Concesso per il **sysadmin** ruolo predefinito del server e il **DatabaseMailUserRole** ruolo predefinito del database. Quando viene utilizzata da un membro del **sysadmin** ruolo predefinito del server, questa visualizzazione Mostra tutti gli allegati. Tutti gli altri utenti vedono semplicemente gli allegati dei messaggi che hanno inviato personalmente.  
  
## <a name="see-also"></a>Vedere anche  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
