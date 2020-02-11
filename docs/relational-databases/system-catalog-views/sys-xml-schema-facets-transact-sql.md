---
title: sys. xml_schema_facets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41e00ca05205fcb1384d436de2f423c63e05ba5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103357"
---
# <a name="sysxml_schema_facets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per facet (restrizione) di una definizione di tipo XML (corrisponde a **sys. xml_types**).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|ID del componente XML (tipo) a cui appartiene il facet corrente.|  
|**facet_id**|**int**|ID (ordinale in base 1) del facet, univoco all'interno dell'ID del componente.|  
|**tipo**|**carattere (2)**|Tipo di facet:<br /><br /> LG = Lunghezza (Length)<br /><br /> LN = Lunghezza minima (Minimum Length)<br /><br /> LX = Lunghezza massima (Maximum Length)<br /><br /> PT = Pattern (espressione regolare)<br /><br /> EU = Enumerazione (Enumeration)<br /><br /> IN = Valore inclusivo minimo (Minimum Inclusive value)<br /><br /> IX = Valore inclusivo massimo (Maximum Inclusive value)<br /><br /> EN = Valore esclusivo minimo (Minimum Exclusive value)<br /><br /> EX = Valore esclusivo massimo (Maximum Exclusive value)<br /><br /> DT = Totale cifre (Total Digits)<br /><br /> DF = Cifre frazionarie (Fraction Digits)<br /><br /> WS = Normalizzazione di spazi vuoti (White Space normalization)|  
|**kind_desc**|**nvarchar (60)**|Descrizione del tipo di facet:<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = Il facet include un valore fisso predefinito.<br /><br /> 0 = Nessun valore fisso (predefinito)|  
|**valore**|**nvarchar (4000)**|Valore fisso predefinito del facet.|  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]Per altre informazioni, vedere [configurazione della visibilità dei metadati](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schema &#40;viste del catalogo&#41; di sistema di tipo XML &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
