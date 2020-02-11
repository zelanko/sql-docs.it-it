---
title: sys. sysdevices (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cbd14a7ce8dd1cfb1571874a83a615065200014
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053517"
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni file di backup su disco, di backup su nastro e di database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome logico del file di backup o di database.|  
|**dimensioni**|**int**|Dimensioni del file in pagine da 2 KB.|  
|**basso**|**int**|Supportata per compatibilità con le versioni precedenti.|  
|**alta**|**int**|Supportata per compatibilità con le versioni precedenti.|  
|**stato**|**smallint**|Mappa di bit che indica il tipo di dispositivo:<br /><br /> 1 = disco predefinito<br /><br /> 2 = disco fisico<br /><br /> 4 = disco logico<br /><br /> 8 = ignora intestazione<br /><br /> 16 = file di backup<br /><br /> 32 = scritture in serie<br /><br /> 4096= sola lettura|  
|**CntrlType**|**smallint**|Tipo di controller:<br /><br /> 0 = file di database non CD-ROM<br /><br /> 2 = file di backup su disco<br /><br /> 3 - 4 = file di backup su dischetto<br /><br /> 5 = file di backup su nastro<br /><br /> 6 = file named pipe|  
|**phyname**|**nvarchar(260)**|Nome del file fisico.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
