---
title: CONSTRAINT_TABLE_USAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TABLE_USAGE_TSQL
- CONSTRAINT_TABLE_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- CONSTRAINT_TABLE_USAGE view
- INFORMATION_SCHEMA.CONSTRAINT_TABLE_USAGE view
ms.assetid: 5770b696-6c04-4d5c-a8db-9eb92022fa42
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ea6558701546b68c0c5ee1876cb127ba7bba054
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132931"
---
# <a name="constrainttableusage-transact-sql"></a>CONSTRAINT_TABLE_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tabella del database corrente in cui è definito un vincolo. Questa vista degli schemi delle informazioni restituisce informazioni sugli oggetti per i quali l'utente dispone di autorizzazioni.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificatore della tabella.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome dello schema che contiene la tabella.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Qualificatore del vincolo.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nome dello schema che contiene il vincolo.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome del vincolo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys. Foreign_Keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
