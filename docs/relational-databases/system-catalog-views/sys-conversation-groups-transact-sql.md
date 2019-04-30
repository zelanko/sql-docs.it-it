---
title: sys.conversation_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_groups_TSQL
- conversation_groups
- sys.conversation_groups
- sys.conversation_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_groups catalog view
ms.assetid: 3f35815e-2de4-42a2-a972-8f0141dad0b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01e6e1d47061f445d7aa7d53fb548a2ebfcaefd6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049862"
---
# <a name="sysconversationgroups-transact-sql"></a>sys.conversation_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa vista del catalogo contiene una riga per ogni gruppo di conversazioni.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**conversation_group_id**|**uniqueidentifier**|Identificatore del gruppo di conversazioni. Non ammette i valori Null.|  
|**service_id**|**int**|Identificatore del servizio per le conversazioni nel gruppo. Non ammette i valori Null.|  
|**is_system**|**bit**|Indica se si tratta di un'istanza di sistema. Ammette valori Null.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
