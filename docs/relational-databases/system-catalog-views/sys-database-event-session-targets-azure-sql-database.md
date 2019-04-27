---
title: Sys. database_event_session_targets (Database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8828532142bbcd8c188286ba87c16c3b824a279c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62751539"
---
# <a name="sysdatabaseeventsessiontargets-azure-sql-database"></a>sys.database_event_session_targets (database SQL di Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni destinazione di evento per una sessione eventi.  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Versione 12 e tutte le versioni successive.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|ID della sessione dell'evento. Non ammette i valori Null.|  
|target_id|**int**|ID della destinazione. L'ID è univoco all'interno dell'oggetto della sessione dell'evento. Non ammette i valori Null.|  
|NAME|**sysname**|Nome della destinazione dell'evento. Non ammette i valori Null.|  
|pacchetto|**sysname**|Nome del pacchetto dell'evento contenente la destinazione dell'evento. Non ammette i valori Null.|  
|modulo|**sysname**|Nome del modulo contenente la destinazione dell'evento. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE per il server.  
  
## <a name="remarks"></a>Note  
 Questa vista ha le cardinalità della relazione seguenti.  
  
||||  
|-|-|-|  
|From|Per|Relazione|  
|sys.database_event_session_targets.event_session_id|sys.database_event_sessions.event_session_id|Molti-a-uno|  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
