---
title: sys.service_message_types (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 81a7a5cd518096582ba07e4400982308b9c1c2aa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856635"
---
# <a name="sysservicemessagetypes-transact-sql"></a>sys.service_message_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per tipo di messaggio registrato in Service Broker.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**message_type_id**|**int**|Identificatore del tipo di messaggio, univoco all'interno del database. Non ammette i valori Null.|  
|**principal_id**|**int**|Identificatore dell'entità di database proprietaria del tipo di messaggio. Ammette valori Null.|  
|**validation**|**char(2)**|Convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Non ammette i valori Null. I possibili valori sono i seguenti:<br /><br /> N = Nessuno<br /><br /> X = XML<br /><br /> E = Vuoto|  
|**validation_desc**|**nvarchar(60)**|Descrizione della convalida eseguita da Service Broker prima dell'invio di messaggi del tipo specificato. Ammette valori Null. I possibili valori sono i seguenti:<br /><br /> Nessuno<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|Per la convalida che utilizza un XML Schema, identificatore per la raccolta di schemi utilizzata.<br /><br /> In caso contrario, NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
