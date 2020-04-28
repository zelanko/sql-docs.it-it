---
title: sys. security_policies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d6eec5c523e2bdd321af145f19d0b5e7e7cba39b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135307"
---
# <a name="syssecurity_policies-transact-sql"></a>sys. security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Restituisce una riga per ogni criterio di sicurezza nel database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome del criterio di sicurezza, univoco all'interno del database.|  
|object_id|**int**|ID del criterio di sicurezza.|  
|principal_id|**int**|ID del proprietario del criterio di sicurezza registrato nel database. NULL se il proprietario viene determinato tramite lo schema.|  
|schema_id|**int**|ID dello schema in cui si trova l'oggetto.|  
|parent_object_id|**int**|ID dell'oggetto a cui appartiene il criterio. Deve essere 0.|  
|type|**vachar (2)**|Deve essere **SP**.|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**.|  
|create_date|**datetime**|Data UTC di creazione del criterio di sicurezza.|  
|modify_date|**datetime**|Data UTC dell'ultima modifica del criterio di sicurezza.|  
|is_ms_shipped|**bit**|Sempre false.|  
|is_enabled|**bit**|Stato della specifica del criterio di sicurezza:<br /><br /> 0 = disabilitato<br /><br /> 1 = abilitato|  
|is_not_for_replication|**bit**|Il criterio è stato creato con l'opzione NOT FOR REPLICATION.|  
|uses_database_collation|**bit**|Usa le stesse regole di confronto del database.|  
|is_schemabinding_enabled|**bit**|Stato schema per i criteri di sicurezza:<br /><br /> 0 o NULL = abilitato<br /><br /> 1 = disabilitato|  
  
## <a name="permissions"></a>Autorizzazioni  
 Le entità con l'autorizzazione **ALTER ANY Security Policy** possono accedere a tutti gli oggetti in questa vista del catalogo, nonché a qualsiasi utente con la **definizione della vista** sull'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza a livello di riga](../../relational-databases/security/row-level-security.md)   
 [sys. security_predicates &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREARE criteri di sicurezza &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Viste del catalogo di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
