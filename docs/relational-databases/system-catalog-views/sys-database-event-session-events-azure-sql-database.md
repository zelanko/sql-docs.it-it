---
description: sys.database_event_session_events (database SQL di Azure)
title: sys.database_event_session_events (database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: f4c9eb0a-173c-4c66-8dd8-6f7176b2657f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 99c8cf898c8e7ee719af0a88b7c2ea80a7e1ec83
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97458938"
---
# <a name="sysdatabase_event_session_events-azure-sql-database"></a>sys.database_event_session_events (database SQL di Azure)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Restituisce una riga per ogni evento in una sessione di eventi.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 e a tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|event_id|**int**|ID dell'evento. L'ID è univoco all'interno dell'oggetto della sessione dell'evento. Non ammette i valori Null.|  
|name|**sysname**|Nome dell'evento. Non ammette i valori Null.|  
|Pacchetto|**sysname**|Nome del pacchetto eventi che contiene l'evento. Non ammette i valori Null.|  
|module|**sysname**|Nome del modulo contenente l'evento. Non ammette i valori Null.|  
|predicate|**nvarchar (3000)**|Espressione del predicato applicata all'evento. Ammette i valori Null.|  
|predicate_xml|**nvarchar (3000)**|Espressione del predicato XML applicata all'evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il server.  
  
## <a name="remarks"></a>Commenti  
 Questa vista ha le cardinalità della relazione seguenti.  
  
| Da | A | Relazione |
| ---- | -- | ------------ |
|sys.database_event_session_events sys.database_event_session_events.event_session_id|sys.database_event_sessions sys.database_event_sessions.event_session_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
