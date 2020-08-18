---
description: sys.cryptographic_providers (Transact-SQL)
title: sys. cryptographic_providers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cryptographic_providers
- sys.cryptographic_providers
- sys.cryptographic_providers_TSQL
- cryptographic_providers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.cryptographic_providers catalog view
ms.assetid: 9da0da95-792e-48b4-9f60-47f0729c279c
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 898522531177d562ce15f81512efd49b47762958
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88402397"
---
# <a name="syscryptographic_providers-transact-sql"></a>sys.cryptographic_providers (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce una riga per ogni provider di crittografia registrato.  
    
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|Numero di identificazione del provider di crittografia.|  
|**nome**|**sysname**|Nome del provider di crittografia.|  
|**guid**|**uniqueidentifier**|GUID univoco del provider.|  
|**version**|**nvarchar(50)**|Versione del provider nel formato '*AA.BB.cccc.dd*'.|  
|**dll_path**|**nvarchar(512)**|Percorso della DLL che implementa l'API (Application Program Interface) dell'EKM (Extensible Key Management).|  
|**is_enabled**|**bit**|Specifica se il provider è abilitato o meno nel server.<br /><br /> 0 = non abilitato (predefinito)<br /><br /> 1 = abilitato|  
  
## <a name="remarks"></a>Osservazioni  
 La vista **sys. cryptographic_providers** è visibile al pubblico.  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
  
