---
title: Interpretazione delle annotazioni (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2db54a2bec501c3422cf19b1efab7cdb581420e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013444"
---
# <a name="annotation-interpretation-sqlxml-40"></a>Interpretazione delle annotazioni (SQLXML 4.0)
  Negli argomenti riportati in questa sezione viene descritto in che modo il caricamento bulk XML interpreta le annotazioni nello schema XSD. Il comportamento descritto è applicabile anche alle annotazioni nello schema XDR.  
  
> [!NOTE]  
>  Nelle informazioni contenute in questi argomenti vengono descritte solo le annotazioni utilizzate durante l'elaborazione del caricamento bulk XML. Per un elenco completo delle annotazioni per lo schema XSD supportate da SQLXML 4,0, vedere [utilizzo di annotazioni negli schemi xsd &#40;sqlxml 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md). Per un elenco delle annotazioni supportate per gli schemi XDR, vedere la pagina relativa agli [schemi XDR con Annotazioni &#40;deprecati in SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [SQL: relationship e regola di ordinamento delle chiavi &#40;SQLXML 4,0&#41;](annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 Viene descritto in che modo l'annotazione `sql:relationship` viene interpretata nel caricamento bulk XML.  
  
 [SQL: mappato &#40;SQLXML 4,0&#41;](annotation-interpretation-sql-mapped.md)  
 Viene descritto in che modo l'annotazione `sql:mapped` viene interpretata nel caricamento bulk XML.  
  
 [SQL: limit-field e SQL: Limit-Value &#40;SQLXML 4,0&#41;](annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Viene descritto in che modo le annotazioni `sql:limit-field` e `sql:limit-value` vengono interpretate nel caricamento bulk XML.  
  
 [SQL: overflow-field &#40;SQLXML 4,0&#41;](annotation-interpretation-sql-overflow-field.md)  
 Viene descritto in che modo l'annotazione `sql:overflow` viene interpretata nel caricamento bulk XML.  
  
 [Altre annotazioni &#40;SQLXML 4,0&#41;](annotation-interpretation-other-annotations.md)  
 Viene descritto in che modo le annotazioni seguenti vengono interpretate nel caricamento bulk XML: `sql:id-prefix`, `sql:use-cdata`, `sql:url-encode`, `sql:is-mapping-schema`, `sql:key-fields`.  
  
  
