---
description: VIEWS (Transact-SQL)
title: VISTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1ee6ebd84d20b15d104bb7ecde412e5725deef9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536832"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Restituisce una riga per le viste a cui l'utente corrente può accedere nel database corrente.  
  
 Per recuperare informazioni da queste viste, specificare il nome completo del **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificatore della vista.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome dello schema che contiene la vista.<br /><br /> **&#42;&#42; importante &#42;&#42;**  solo il modo affidabile per trovare lo schema di un oggetto consiste nell'eseguire una query sulla vista del catalogo sys. Objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nome della vista.|  
|**VIEW_DEFINITION**|**nvarchar (** 4000 **)**|Se la lunghezza della definizione è maggiore di **nvarchar (** 4000 **)**, questa colonna è null. In caso contrario, questa colonna corrisponde al testo della definizione della vista.|  
|**CHECK_OPTION**|**varchar (** 7 **)**|Tipo di WITH CHECK OPTION. Restituisce CASCADE se la vista originale è stata creata tramite WITH CHECK OPTION. In caso contrario restituisce NONE.|  
|**IS_UPDATABLE**|**varchar (** 2 **)**|Specifica se è possibile aggiornare la vista. Restituisce sempre NO.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Viste degli schemi delle informazioni &#40;&#41;Transact-SQL ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
