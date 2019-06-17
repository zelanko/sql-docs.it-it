---
title: sys.server_event_notifications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b985d915d3d7bb6b3130ccb63a400f314fa05a38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860908"
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni oggetto notifica degli eventi a livello del server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome della notifica degli eventi a livello del server. Tale nome è univoco tra tutte le notifiche degli eventi a livello del server.|  
|**object_id**|**int**|Numero di identificazione dell'oggetto. È univoco all'interno di **master** database.|  
|**parent_class**|**tinyint**|Classe padre. È sempre 100 = Server.|  
|**parent_class_desc**|**nvarchar(60)**|Descrizione della classe padre. È sempre SERVER.|  
|**parent_id**|**int**|È sempre 0.|  
|**create_date**|**datetime**|Data di creazione.|  
|**modify_date**|**datetime**|Data dell'ultima modifica dell'oggetto con un'istruzione ALTER.|  
|**service_name**|**nvarchar(256)**|Nome del servizio di destinazione a cui viene inviata la notifica.|  
|**broker_instance**|**nvarchar(128)**|Istanza di Service Broker in cui è definito il servizio di destinazione specificato.|  
|**creator_sid**|**varbinary(85)**|SID dell'account di accesso che esegue l'istruzione per la creazione della notifica degli eventi. È NULL se nella definizione di notifica degli eventi non si specifica WITH FAN_IN.|  
|**principal_id**|**int**|ID dell'entità server proprietaria dell'oggetto.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
