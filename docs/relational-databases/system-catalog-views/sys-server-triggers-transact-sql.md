---
title: Sys. server_triggers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_triggers
- sys.server_triggers_TSQL
- server_triggers_TSQL
- sys.server_triggers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_triggers catalog view
ms.assetid: 25926ff4-9271-45bf-bc32-d5d3344bd47a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 995a9b5fe4786e1e188a8bbdc612cce743e77a18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133010"
---
# <a name="sysservertriggers-transact-sql"></a>sys.server_triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include il set di tutti i trigger DDL a livello di server con object_type TR o TA. In caso di trigger CLR, l'assembly deve essere caricato nel **master** database. Tutti i nomi dei trigger DDL a livello di server esistono in un singolo ambito globale.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del trigger.|  
|**object_id**|**int**|ID dell'oggetto.|  
|**parent_class**|**tinyint**|Classe padre. È sempre:<br /><br /> 100 = Server|  
|**parent_class_desc**|**nvarchar(60)**|Descrizione della classe padre. È sempre:<br /><br /> SERVER.|  
|**parent_id**|**int**|Sempre 0 per i trigger nel SERVER.|  
|**type**|**char(2)**|Tipo di oggetto:<br /><br /> TA = Trigger di assembly (CLR)<br /><br /> TR = trigger SQL|  
|**type_desc**|**nvarchar(60)**|Descrizione della classe del tipo di oggetto.<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**create_date**|**datetime**|Data di creazione del trigger.|  
|**modify_date**|**datetime**|Data dell'ultima modifica del trigger tramite un'istruzione ALTER.|  
|**is_ms_shipped**|**bit**|Trigger creato per conto dell'utente da parte di un componente interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_disabled**|**bit**|1 = il trigger è disabilitato.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
