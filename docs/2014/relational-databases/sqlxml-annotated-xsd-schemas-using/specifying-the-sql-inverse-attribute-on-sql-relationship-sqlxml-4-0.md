---
title: "Specifica dell'attributo SQL: inverse in SQL: Relationship (SQLXML 4,0) | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 90c2b7836de03369c09d68181fd1cb61b355107b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703484"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Specifica dell'attributo sql:inverse in sql:relationship (SQLXML 4.0)
  L'attributo `sql:inverse` risulta utile solo quando lo schema XSD viene utilizzato per il caricamento bulk o da un updategram. L' `sql:inverse` attributo può essere specificato nell'elemento ** \< sql: Relationship>** . Negli updategram la relativa logica interpreta lo schema nella determinazione delle tabelle e delle colonne aggiornate dall'operazione dell'updategram. Le relazioni padre-figlio specificate nello schema determinano l'ordine di modifica (inserimento o eliminazione) dei record.  
  
 Nel caso di uno schema XSD in cui la relazione padre-figlio viene specificata nell'ordine inverso a quello della relazione chiave primaria/chiave esterna tra le colonne del database corrispondenti, l'operazione di inserimento o eliminazione dell'updategram non riuscirà a causa della violazione della relazione chiave primaria/chiave esterna. In questi casi, l' `sql:inverse` attributo viene specificato ( `sql:inverse="true"` ) nell'elemento ** \< SQL: Relationship>** e la logica dell'updategram inverte l'interpretazione della relazione padre-figlio specificata nello schema.  
  
 L'attributo `sql:inverse` utilizza un valore booleano (0=false, 1=true). I valori possibili sono 0, 1, true e false.  
  
 Per un esempio funzionante di utilizzo dell' `sql:inverse` annotazione, vedere [specifica di uno schema di mapping con annotazioni in un updategram](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione di relazioni tramite SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
