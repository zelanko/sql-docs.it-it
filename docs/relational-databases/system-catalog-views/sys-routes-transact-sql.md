---
title: sys. Routes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- routes
- routes_TSQL
- sys.routes
- sys.routes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.routes catalog view
ms.assetid: 8fc65915-8bd6-425b-95d9-6a8468cb1e48
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bfdd322107da1a08edb3933aee9d5b79b6c2b47a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67904432"
---
# <a name="sysroutes-transact-sql"></a>sys.routes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per route. Le route vengono utilizzate da Service Broker per individuare l'indirizzo di rete per un servizio.   

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome della route, univoco all'interno del database. Non ammette i valori Null.|  
|**route_id**|**int**|Identificatore della route. Non ammette i valori Null.|  
|**principal_id**|**int**|Identificatore dell'entità di database proprietaria della route. Ammette valori Null.|  
|**remote_service_name**|**nvarchar(256)**|Nome del servizio remoto. Ammette valori Null.|  
|**broker_instance**|**nvarchar(128)**|Identificatore dell'istanza di Service Broker che ospita il servizio remoto. Ammette valori Null.|  
|**vita**|**datetime**|Data e ora di scadenza della route. Questo valore non utilizza il fuso orario locale, bensì corrisponde all'ora di scadenza per UTC. Ammette valori Null.|  
|**address**|**nvarchar(256)**|Indirizzo di rete a cui Service Broker invia messaggi per il servizio remoto. Ammette valori Null. Per Istanza gestita di database SQL, l'indirizzo deve essere locale.|  
|**mirror_address**|**nvarchar(256)**|Indirizzo di rete del partner per il mirroring per il server specificato nell'indirizzo. Ammette valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Per altre informazioni, vedere [configurazione della visibilità dei metadati](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
