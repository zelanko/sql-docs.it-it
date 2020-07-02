---
title: Interpretazione delle annotazioni (SQLXML)
description: Informazioni sul modo in cui il caricamento bulk XML in SQLXML 4,0 interpreta le annotazioni negli schemi XSD e XDR.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 41cb1a0e65b7e453f408a43b71b1cad831b0cba4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790887"
---
# <a name="annotation-interpretation-sqlxml-40"></a>Interpretazione delle annotazioni (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Negli argomenti riportati in questa sezione viene descritto in che modo il caricamento bulk XML interpreta le annotazioni nello schema XSD. Il comportamento descritto è applicabile anche alle annotazioni nello schema XDR.  
  
> [!NOTE]  
>  Nelle informazioni contenute in questi argomenti vengono descritte solo le annotazioni utilizzate durante l'elaborazione del caricamento bulk XML. Per un elenco completo delle annotazioni per lo schema XSD supportate da SQLXML 4,0, vedere [utilizzo di annotazioni negli schemi xsd &#40;sqlxml 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md). Per un elenco delle annotazioni supportate per gli schemi XDR, vedere la pagina relativa agli [schemi XDR con Annotazioni &#40;deprecati in SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [SQL: relationship e regola di ordinamento delle chiavi &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 Viene descritto il modo in cui l'annotazione **SQL: Relationship** viene interpretata nel caricamento bulk XML.  
  
 [SQL: mappato &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 Viene descritto il modo in cui l'annotazione **SQL: mappata** viene interpretata nel caricamento bulk XML.  
  
 [SQL: limit-field e SQL: Limit-Value &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Viene descritto il modo in cui le annotazioni **SQL: limit-field** e **SQL: limit-value** vengono interpretate nel caricamento bulk XML.  
  
 [SQL: overflow-field &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 Viene descritto il modo in cui l'annotazione **SQL: overflow** viene interpretata nel caricamento bulk XML.  
  
 [Altre annotazioni &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 Viene descritto il modo in cui le annotazioni seguenti vengono interpretate nel caricamento bulk XML: **SQL: id-prefix**, **SQL: Use-CDATA**, **SQL: URL-encode**, **SQL: is-mapping-schema**, **SQL: key-fields**.  
  
  
