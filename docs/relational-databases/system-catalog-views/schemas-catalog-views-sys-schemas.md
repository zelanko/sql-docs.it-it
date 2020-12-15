---
description: Viste del catalogo degli schemi-sys. schemas
title: sys. Schemas (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 473dd22d2f19d29e5b778a585ad59d0d99acbaee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479102"
---
# <a name="schemas-catalog-views---sysschemas"></a>Viste del catalogo degli schemi-sys. schemas
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Include una riga per ogni schema di database.  
  
> [!NOTE]  
>  Gli schemi di database sono diversi dagli XML Schema, utilizzati per definire il modello di contenuto dei documenti XML.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**nome**|**sysname**|Nome dello schema. Valore univoco all'interno del database.|  
|**schema_id**|**int**|ID dello schema. Valore univoco all'interno del database.|  
|**principal_id**|**int**|ID dell'entità che possiede lo schema.|  
  
## <a name="remarks"></a>Commenti  
Gli schemi di database fungono da spazi dei nomi o contenitori per oggetti, ad esempio tabelle, viste, procedure e funzioni, che è possibile trovare nella vista del catalogo **sys. Objects** .  

Ogni schema ha un proprietario. Il proprietario è un' [entità](../../relational-databases/security/authentication-access/principals-database-engine.md)di sicurezza.
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo **public** . Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
[Entità](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Viste del catalogo degli schemi &#40;&#41;Transact-SQL ](./catalog-views-transact-sql.md)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
