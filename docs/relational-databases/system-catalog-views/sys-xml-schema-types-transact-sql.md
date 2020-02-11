---
title: sys. xml_schema_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a78730509cc1f9eeec83b8d9ff9cb0917e0ed99
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68060432"
---
# <a name="sysxml_schema_types-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni componente XML Schema che è un tipo **symbol_space** di **T**.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**\<colonne ereditate>**||Eredita le colonne da [sys. xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_abstract**|**bit**|1 = Il tipo è un tipo abstract. Tutte le istanze di un elemento di questo tipo devono utilizzare **xsi: Type** per indicare un tipo derivato non astratto.<br /><br /> 0 = Il tipo non è abstract (predefinito)|  
|**allows_mixed_content**|**bit**|1 = Il contenuto misto è consentito.<br /><br /> 0 = Il contenuto misto non è consentito (predefinito)|  
|**is_extension_blocked**|**bit**|1 = la sostituzione con un'estensione del tipo è bloccata nelle istanze quando l'attributo block nella definizione **complexType** o l'attributo **blockDefault** dello schema predecessore \<> elemento informazioni elemento è impostato su "extension" o "#all".<br /><br /> 0 = La sostituzione con l'estensione non è bloccata.|  
|**is_restriction_blocked**|**bit**|1 = la sostituzione con una restrizione del tipo è bloccata nelle istanze quando l'attributo block nella definizione **complexType** o l'attributo **blockDefault** dello schema predecessore \<> elemento informazioni elemento è impostato su "restriction" o "#all".<br /><br /> 0 = La sostituzione con la restrizione non è bloccata (predefinito)|  
|**is_final_extension**|**bit**|1 = la derivazione per estensione del tipo è bloccata quando l'attributo final nella definizione **complexType** o l'attributo **finalDefault** dello schema predecessore \<> elemento informazioni sugli elementi è impostato su "extension" o "#all".<br /><br /> 0 = L'estensione è consentita (predefinito)|  
|**is_final_restriction**|**bit**|1 = la derivazione per restrizione del tipo è bloccata quando l'attributo final nella definizione semplice o **complexType** o l'attributo **finalDefault** dello schema \<predecessore> elemento informazioni sugli elementi è impostato su "restriction" o "#all".<br /><br /> 0 = La restrizione è consentita (predefinito)|  
|**is_final_list_member**|**bit**|1 = Questo tipo semplice non può essere utilizzato come tipo di elemento in un elenco.<br /><br /> 0 = Questo è un tipo complesso oppure il tipo può essere utilizzato come tipo di elemento (predefinito)|  
|**is_final_union_member**|**bit**|1 = Questo tipo semplice non può essere utilizzato come tipo di membro di Tipo unione.<br /><br /> 0 = Questo è un tipo complesso oppure il tipo può essere utilizzato come tipo di membro unione. (predefinito)|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Per altre informazioni, vedere [configurazione della visibilità dei metadati](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schema &#40;viste del catalogo&#41; di sistema di tipo XML &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
