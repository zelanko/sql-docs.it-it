---
title: sys. messages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- messages_TSQL
- sys.messages_TSQL
- sys.messages
- messages
dev_langs:
- TSQL
helpviewer_keywords:
- error messages [SQL Server]
- sys.messages catalog view
- error numbers [SQL Server]
ms.assetid: 8c16ecdf-68f4-4a2a-b594-086e3344e58a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 44ab2e3106610f7b7130f997e9641e4aba685fd1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127926"
---
# <a name="messages-for-errors-catalog-views---sysmessages"></a>Viste del catalogo per i messaggi (di errore) - Sys.messages
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni **message_id** o **language_id** dei messaggi di errore nel sistema, per i messaggi definiti dall'utente e definiti dal sistema. Per altre informazioni, vedere [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
   
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**message_id**|**int**|ID del messaggio. Questo valore è univoco nel server. I messaggi con ID minore di 50000 sono messaggi di sistema.|  
|**language_id**|**smallint**|ID lingua per cui viene usato il testo in **testo** , come definito in **syslanguages**. Questa operazione è univoca per un **message_id**specificato.|  
|**severity**|**tinyint**|Livello di gravità del messaggio, compreso tra 1 e 25. Questo è lo stesso per tutte le lingue dei messaggi all'interno di un **message_id**.|  
|**is_event_logged**|**bit**|1 = Il messaggio viene registrato nell'evento se viene generato un errore. Questo è lo stesso per tutte le lingue dei messaggi all'interno di un **message_id**.|  
|**text**|**nvarchar(2048)**|Testo del messaggio utilizzato quando è attiva la **language_id** corrispondente.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** .  Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Messaggi &#40;per errori&#41; viste del catalogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)   
 [Programmazione della finestra di messaggio eccezione](https://msdn.microsoft.com/library/0b1ba514-6959-4e69-bfd2-3cf3c1ac4b9c)   
 [Messaggi di errore](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [Eventi ed errori di Motore di database](../../relational-databases/errors-events/database-engine-events-and-errors.md)  
  
  
