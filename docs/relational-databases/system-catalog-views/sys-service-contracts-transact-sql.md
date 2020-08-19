---
description: sys.service_contracts (Transact-SQL)
title: sys. service_contracts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contracts_TSQL
- sys.service_contracts_TSQL
- sys.service_contracts
- service_contracts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contracts catalog view
ms.assetid: 787dd47e-4210-439d-9c4a-57a727a0dbd8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c8a15b21c79cf8f27c8fcdc6c5f3cf88ac35235
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490130"
---
# <a name="sysservice_contracts-transact-sql"></a>sys.service_contracts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Questa vista del catalogo contiene una riga per ogni contratto nel database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome del contratto, univoco all'interno del database. Non ammette i valori Null.|  
|**service_contract_id**|**int**|Identificatore del contratto. Non ammette i valori Null.|  
|**principal_id**|**int**|Identificatore dell'entità di database proprietaria del contratto. Ammette valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
