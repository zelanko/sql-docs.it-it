---
description: sys.sysperfinfo (Transact-SQL)
title: sys.sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
ms.openlocfilehash: 1122c224e21fa633c2c04cd156a49878fefc7daa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482104"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rappresentazione dei contatori delle prestazioni interni che possono essere visualizzati tramite il monitor di sistema di Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar (128)**|Nome dell'oggetto prestazioni, ad esempio **SqlServer: LockManager** o **SqlServer: gestore buffer**.|  
|**counter_name**|**nchar (128)**|Nome del contatore delle prestazioni all'interno dell'oggetto, ad esempio **richieste di pagine** o **blocchi richiesti**.|  
|**instance_name**|**nchar (128)**|Istanza denominata del contatore. Sono ad esempio presenti contatori mantenuti per ogni tipo di blocco, ad esempio **tabelle**, **pagine**, **chiavi**e così via. Il nome dell'istanza consente di contraddistinguere contatori simili.|  
|**cntr_value**|**bigint**|Valore effettivo del contatore. Spesso si tratta di un contatore a incremento progressivo costante che conta le occorrenze dell'evento dell'istanza.|  
|**cntr_type**|**int**|Tipo di contatore definito dall'architettura di controllo delle prestazioni di Windows.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste della compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
