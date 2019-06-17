---
title: sys.schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8519dc4846f148b1b4d1bc83589baf0cc6a81e12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983141"
---
# <a name="schemas-catalog-views---sysschemas"></a>Schemi - vista del catalogo sys. Schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Include una riga per ogni schema di database.  
  
> [!NOTE]  
>  Gli schemi di database sono diversi dagli XML Schema, utilizzati per definire il modello di contenuto dei documenti XML.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome dello schema. Valore univoco all'interno del database.|  
|**schema_id**|**int**|ID dello schema. Valore univoco all'interno del database.|  
|**principal_id**|**int**|ID dell'entità che possiede lo schema.|  
  
## <a name="remarks"></a>Note  
Gli schemi di database fungono da spazi dei nomi o contenitori per gli oggetti, ad esempio tabelle, viste, procedure e funzioni, che possono essere trovati nel **Sys. Objects** vista del catalogo.  

Ogni schema ha un proprietario. Il proprietario è un security [principal](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
[Entità](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Viste del catalogo schemi &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
