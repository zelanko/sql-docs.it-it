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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 560ee8a4ccc03f747df2b475394af092db589e7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68078744"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per tipo di messaggio registrato in Service Broker.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**message_type_id**|**int**|Identificatore del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**principal_id**|**int**|Identificatore dell'entità di database proprietaria del tipo di messaggio. Ammette valori Null.|  
|**convalida**|**char(2)**|Convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Non ammette i valori Null. Uno dei valori possibili:<br /><br /> N = Nessuno<br /><br /> X = XML<br /><br /> E = Vuoto|  
|**validation_desc**|**nvarchar(60)**|Descrizione della convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Ammette valori Null. Uno dei valori possibili:<br /><br /> NONE<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|Per la convalida che utilizza un XML Schema, identificatore per la raccolta di schemi utilizzata.<br /><br /> In caso contrario, NULL.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
