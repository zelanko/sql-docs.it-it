---
title: sys. server_triggers (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b7a0a99f46cdd3ec5d2b6b9ac96cae7a1dc5c55e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832723"
---
# <a name="sysserver_triggers-transact-sql"></a>sys.server_triggers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Include il set di tutti i trigger DDL a livello di server con object_type TR o TA. Nel caso dei trigger CLR, l'assembly deve essere caricato nel database **Master** . Tutti i nomi dei trigger DDL a livello di server esistono in un singolo ambito globale.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del trigger.|  
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
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
