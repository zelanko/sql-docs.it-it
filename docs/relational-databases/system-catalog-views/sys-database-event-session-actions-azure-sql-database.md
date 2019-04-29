---
title: Sys. database_event_session_actions (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da64525978a5655df1832d70959929d6221c9a7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936314"
---
# <a name="sysdatabaseeventsessionactions-azure-sql-database"></a>sys.database_event_session_actions (database SQL di Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni azione su ogni evento di una sessione dell'evento.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Versione 12 e tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|event_id|**int**|ID dell'evento. L'ID è univoco all'interno dell'oggetto della sessione di evento. Non ammette i valori Null.|  
|NAME|**sysname**|Nome dell'azione. Ammette i valori Null.|  
|pacchetto|**sysname**|Nome del pacchetto eventi che contiene l'evento. Ammette i valori Null.|  
|modulo|**sysname**|Nome del modulo contenente l'evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il server.  
  
## <a name="remarks"></a>Note  
 Questa vista ha le cardinalità della relazione seguenti.  
  
||||  
|-|-|-|  
|From|Per|Relazione|  
|sys.database_event_session_actions.event_session_id|sys.sys.database_event_sessions.event_session_id|Molti-a-uno|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Molti-a-uno|  
  
  
