---
title: sys. Assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assemblies
- assemblies_TSQL
- sys.assemblies_TSQL
- assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assemblies catalog view
ms.assetid: e321753f-293f-42ab-b225-d118713df40b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5b430767a7ded990b440c3f22b68c2bfab2573a
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394833"
---
# <a name="sysassemblies-transact-sql"></a>sys.assemblies (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Restituisce una riga per ogni assembly.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome dell'assembly. Valore univoco all'interno del database.|  
|**principal_id**|**int**|ID dell'entità proprietaria dell'assembly.|  
|**assembly_id**|**int**|Numero di identificazione dell'assembly. Valore univoco all'interno di un database.|  
|**clr_name**|**nvarchar(4000)**|Stringa canonica che codifica il nome semplice, il numero di versione, le impostazioni internazionali, la chiave pubblica e l'architettura dell'assembly. Questo valore identifica in modo univoco l'assembly sul lato CLR (Common Language Runtime).|  
|**permission_set**|**tinyint**|Set di autorizzazioni o livello di sicurezza dell'assembly.<br /><br /> 1 = Accesso sicuro<br /><br /> 2 = Accesso esterno<br /><br /> 3 = Accesso non sicuro|  
|**permission_set_desc**|**nvarchar(60)**|Descrizione del set di autorizzazioni o del livello di sicurezza dell'assembly.<br /><br /> SAFE_ACCESS<br /><br /> EXTERNAL_ACCESS<br /><br /> UNSAFE_ACCESS|  
|**is_visible**|**bit**|1 = L'assembly è visibile per la registrazione di punti di ingresso [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> 0 = L'assembly è destinato unicamente a chiamanti gestiti, ovvero fornisce un'implementazione interna per altri assembly del database.|  
|**create_date**|**datetime**|Data di creazione o registrazione dell'assembly.|  
|**modify_date**|**datetime**|Data di modifica dell'assembly.|  
|**is_user_defined**|**bit**|Indica l'origine dell'assembly.<br /><br /> 0 = assembly definiti dal sistema, ad esempio Microsoft. SqlServer. Types per il tipo di dati **hierarchyid**<br /><br /> 1 = Assembly definiti dall'utente|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Viste del catalogo degli assembly CLR &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;&#41;Transact-SQL](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
