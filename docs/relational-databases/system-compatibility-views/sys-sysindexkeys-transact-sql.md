---
description: sys.sysindexkeys (Transact-SQL)
title: sys.sysindexkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysindexkeys
- sys.sysindexkeys_TSQL
- sysindexkeys_TSQL
- sys.sysindexkeys
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexkeys system table
- sys.sysindexkeys compatibility view
ms.assetid: 53a33c8d-e5f0-430d-a712-b65f43d64318
author: rothja
ms.author: jroth
ms.openlocfilehash: 8934f884ba5a0841ab54a2a06bafbe3d654e6bcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469895"
---
# <a name="syssysindexkeys-transact-sql"></a>sys.sysindexkeys (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene informazioni relative alle chiavi o alle colonne di un indice del database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID della tabella.|  
|**indid**|**smallint**|ID dell'indice.|  
|**colid**|**smallint**|ID della colonna.|  
|**keyno**|**smallint**|Posizione della colonna nell'indice.|  
  
## <a name="see-also"></a>Vedere anche  
 [Mapping di tabelle di sistema a viste di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Viste di compatibilità &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
