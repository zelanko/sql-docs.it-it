---
title: Impostare l'attributo sql:inverse in sql:relationship (SQLXML)Set sql:inverse attribute on sql:relationship (SQLXML)
description: Informazioni su come usare l'attributo sql:inverse nell'elemento sql:relationship per specificare le relazioni tra le colonne del database in un'operazione updategram.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe5409120a3d0c5df3cf05318b0b85fd22d07bdf
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388098"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Specifica dell'attributo sql:inverse in sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  L'attributo **sql:inverse** è utile solo quando lo schema XSD viene utilizzato per il caricamento bulk o da un updategram. L'attributo **sql:inverse** può essere specificato nell'elemento ** \<sql:relationship>.** Negli updategram la relativa logica interpreta lo schema nella determinazione delle tabelle e delle colonne aggiornate dall'operazione dell'updategram. Le relazioni padre-figlio specificate nello schema determinano l'ordine di modifica (inserimento o eliminazione) dei record.  
  
 Nel caso di uno schema XSD in cui la relazione padre-figlio viene specificata nell'ordine inverso a quello della relazione chiave primaria/chiave esterna tra le colonne del database corrispondenti, l'operazione di inserimento o eliminazione dell'updategram non riuscirà a causa della violazione della relazione chiave primaria/chiave esterna. In questi casi, l'attributo **sql:inverse** viene specificato (**sql:inverse "true"**) nell'elemento ** \<sql:relationship>** e la logica updategram inversa l'interpretazione della relazione padre-figlio specificata nello schema.  
  
 L'attributo **sql:inverse** accetta un valore booleano (0, false, 1 , true). I valori possibili sono 0, 1, true e false.  
  
 Per un esempio funzionante che utilizza l'annotazione **sql:inverse,** vedere Specifica di uno schema di mapping con [annotazioni in un Updategram](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Specifica di relazioni tramite sql:relationship &#40;&#41;SQLXML 4.0Specifying Relationships Using sql:relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
