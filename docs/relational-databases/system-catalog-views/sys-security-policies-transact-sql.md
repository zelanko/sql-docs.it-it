---
title: Sys. security_policies (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b93943109267db79b1c8475eb3e1875950f9970a
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161788"
---
# <a name="syssecuritypolicies-transact-sql"></a>Sys. security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Restituisce una riga per ogni criterio di sicurezza nel database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|Nome del criterio di sicurezza, univoco all'interno del database.|  
|object_id|**int**|ID del criterio di sicurezza.|  
|principal_id|**int**|ID del proprietario del criterio di sicurezza registrato nel database. NULL se il proprietario viene determinato tramite lo schema.|  
|schema_id|**int**|ID dello schema in cui si trova l'oggetto.|  
|parent_object_id|**int**|ID dell'oggetto a cui appartiene il criterio. Deve essere 0.|  
|Tipo|**vachar(2)**|Deve essere **SP**.|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**.|  
|create_date|**datetime**|Data UTC di creazione del criterio di sicurezza.|  
|modify_date|**datetime**|Data UTC dell'ultima modifica del criterio di sicurezza.|  
|is_ms_shipped|**bit**|Sempre false.|  
|is_enabled|**bit**|Stato della specifica del criterio di sicurezza:<br /><br /> 0 = disabilitato<br /><br /> 1 = abilitato|  
|is_not_for_replication|**bit**|Il criterio è stato creato con l'opzione NOT FOR REPLICATION.|  
|uses_database_collation|**bit**|Usa le stesse regole di confronto del database.|  
|is_schemabinding_enabled|**bit**|SCHEMABINDING dello stato per i criteri di sicurezza:<br /><br /> 0 o NULL = abilitata<br /><br /> 1 = disabilitata|  
  
## <a name="permissions"></a>Permissions  
 Le entità con la **ALTER ANY SECURITY POLICY** autorizzazione ha accesso a tutti gli oggetti in questa vista del catalogo, nonché tutti gli utenti con **VIEW DEFINITION** sull'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza a livello di riga](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
