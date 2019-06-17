---
title: sys.sysmessages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysmessages
- sysmessages
- sysmessages_TSQL
- sys.sysmessages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.sysmessages compatibility view
ms.assetid: 44bee7d9-7517-4071-99be-8b36f979c7cc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cb13b8e57b69c814f18c414dbc345e307d80085c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018696"
---
# <a name="syssysmessages-transact-sql"></a>sys.sysmessages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni avviso o errore di sistema che può essere restituito dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Tramite il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene visualizzata una descrizione dell'errore.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**error**|**int**|Numero univoco dell'errore.|  
|**severity**|**tinyint**|Livello di gravità dell'errore.|  
|**dlevel**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**description**|**nvarchar(255)**|Spiegazione dell'errore in cui i parametri sono rappresentati da segnaposto.|  
|**msglangid**|**smallint**|ID del gruppo di messaggi di sistema.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
