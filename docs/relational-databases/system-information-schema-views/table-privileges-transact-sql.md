---
title: TABLE_PRIVILEGES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- TABLE_PRIVILEGES_TSQL
- TABLE_PRIVILEGES
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_PRIVILEGES view
- TABLE_PRIVILEGES view
ms.assetid: 70269d26-b085-4a98-8a9f-b4742c2848bd
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86bd404320063ec134f18c1707ff8c12470e42a2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783062"
---
# <a name="table_privileges-transact-sql"></a>TABLE_PRIVILEGES (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce una riga per ogni privilegio di tabella concesso a o dall'utente corrente nel database in uso.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**GRANTOR**|**nvarchar (** 128 **)**|Utente che concede il privilegio.|  
|**GRANTEE**|**nvarchar (** 128 **)**|Beneficiario del privilegio.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificatore della tabella.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome dello schema che contiene la tabella.<br /><br /> Importante solo il modo affidabile per trovare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys. Objects. <strong> \* \* \* \* </strong>|  
|**TABLE_NAME**|**sysname**|Nome della tabella.|  
|**PRIVILEGE_TYPE**|**varchar (** 10 **)**|Tipo di privilegio.|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|Specifica se il beneficiario può concedere autorizzazioni ad altri utenti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys. Objects &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. database_permissions &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)  
  
  
