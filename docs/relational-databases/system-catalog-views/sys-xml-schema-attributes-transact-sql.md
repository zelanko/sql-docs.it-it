---
description: sys.xml_schema_attributes (Transact-SQL)
title: sys.xml_schema_attributes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xml_schema_attributes_TSQL
- xml_schema_attributes
- sys.xml_schema_attributes_TSQL
- sys.xml_schema_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_attributes catalog view
ms.assetid: dd0c98aa-5e72-4df6-96d9-482786c8dbb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a64481a5e3ab55a489d173dfd88f295a09aa9dfd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546716"
---
# <a name="sysxml_schema_attributes-transact-sql"></a>sys.xml_schema_attributes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce una riga per XML Schema componente che è un attributo **symbol_space** di **un oggetto**.  

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|Eredita da [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_default_fixed**|**bit**|1 = Il valore predefinito è un valore fisso. Questo valore non può essere sostituito in un'istanza XML.<br /><br /> 0 = Il valore predefinito non è un valore fisso per l'attributo. (predefinito)|  
|**must_be_qualified**|**bit**|1 = L'attributo deve essere qualificato come spazio dei nomi in modo esplicito.<br /><br /> 0 = L'attributo può essere qualificato come spazio dei nomi in modo implicito. (predefinito)|  
|**default_value**|**nvarchar**<br /><br /> **(4000)**|Valore predefinito dell'attributo. È NULL se non viene specificato un valore predefinito.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [XML Schema &#40;viste del catalogo&#41; di sistema di tipo XML &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
