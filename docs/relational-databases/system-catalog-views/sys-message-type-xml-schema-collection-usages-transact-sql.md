---
title: Sys.message_type_xml_schema_collection_usages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages
- message_type_xml_schema_collection_usages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.message_type_xml_schema_collection_usages catalog view
ms.assetid: 544f61a1-c7b7-44b4-bf8d-980ba87d0665
author: stevestein
ms.author: sstein
ms.openlocfilehash: 220f3df2f7bb8ecf0b6acd19f2cec33bf2fc7aa8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125391"
---
# <a name="sysmessagetypexmlschemacollectionusages-transact-sql"></a>sys.message_type_xml_schema_collection_usages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo restituisce una riga per ogni tipo di messaggio di servizio convalidato da una raccolta di XML Schema.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**message_type_id**|**int**|ID del tipo di messaggio di servizio. Non ammette i valori Null.|  
|**xml_collection_id**|**int**|ID della raccolta contenente lo spazio dei nomi dell'XML Schema che esegue la convalida. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
