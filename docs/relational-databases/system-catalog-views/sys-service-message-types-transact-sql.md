---
title: sys. service_message_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7fca6309675975b6c03c46f7724eb6acfe91e580
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752886"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Questa vista del catalogo contiene una riga per tipo di messaggio registrato in Service Broker.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**message_type_id**|**int**|Identificatore del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**principal_id**|**int**|Identificatore dell'entità di database proprietaria del tipo di messaggio. Ammette valori Null.|  
|**validation**|**char(2)**|Convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Non ammette i valori Null. Uno dei valori possibili:<br /><br /> N = Nessuno<br /><br /> X = XML<br /><br /> E = Vuoto|  
|**validation_desc**|**nvarchar(60)**|Descrizione della convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Ammette valori Null. Uno dei valori possibili:<br /><br /> NONE<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|Per la convalida che utilizza un XML Schema, identificatore per la raccolta di schemi utilizzata.<br /><br /> In caso contrario, NULL.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
