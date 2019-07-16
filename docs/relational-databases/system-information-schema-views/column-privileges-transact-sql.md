---
title: COLUMN_PRIVILEGES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMN_PRIVILEGES
- COLUMN_PRIVILEGES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMN_PRIVILEGES view
- INFORMATION_SCHEMA.COLUMN_PRIVILEGES view
ms.assetid: 8ae29a85-2b77-48db-a2b9-a1720287b271
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 703d7cb0b225bf12e7ccd91bdf34251c3044230b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950845"
---
# <a name="columnprivileges-transact-sql"></a>COLUMN_PRIVILEGES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una riga per ogni colonna associata a un privilegio concesso al o dall'utente corrente nel database corrente.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**UTENTE CHE CONCEDE**|**nvarchar(** 128 **)**|Utente che concede il privilegio.|  
|**ALL'UTENTE AUTORIZZATO**|**nvarchar(** 128 **)**|Beneficiario del privilegio.|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|Qualificatore della tabella.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|Nome dello schema che contiene la tabella.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  non utilizzare viste INFORMATION_SCHEMA per determinare lo schema di un oggetto. L'unica modalità affidabile per cercare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**COLUMN_NAME**|**sysname**|Nome colonna.|  
|**PRIVILEGE_TYPE**|**varchar(** 10 **)**|Tipo di privilegio.|  
|**IS_GRANTABLE**|**varchar(** 3 **)**|Specifica se il beneficiario può concedere autorizzazioni ad altri utenti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [Sys. server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
