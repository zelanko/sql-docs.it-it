---
title: numbered_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d0fa4c5ef671d643f85fa2a1a2d0caa62d00d86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68102305"
---
# <a name="sysnumberedprocedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una riga per ogni stored procedure di SQL Server creata come procedura numerata. Non viene visualizzata alcuna riga per la stored procedure di base (numero = 1). Le voci per le stored procedure di base sono disponibili nelle viste, ad esempio **Sys. Objects** e **Procedures**.  
  
> [!IMPORTANT]  
>  Le stored procedure numerate sono deprecate. pertanto non è consigliabile utilizzarle. Un evento DEPRECATION_ANNOUNCEMENT viene generato quando viene compilata una query che utilizza questa vista del catalogo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID dell'oggetto della stored procedure.|  
|**procedure_number**|**smallint**|Numero della procedura nell'oggetto, maggiore o uguale a 2.|  
|**definition**|**nvarchar(max)**|Testo SQL Server che definisce la procedura.<br /><br /> NULL = crittografato.|  
  
> [!NOTE]  
>  I parametri XML e CLR non sono supportati per le stored procedure numerate.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
