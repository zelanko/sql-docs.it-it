---
title: "Impostazione dell'attributo SQL: inverse in SQL: Relationship (SQLXML)"
description: "Informazioni su come usare l'attributo SQL: inverse nell'elemento SQL: Relationship per specificare le relazioni tra le colonne del database in un'operazione updategram."
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b714a70cb3d537d3f9859945b5fdee6842aa5d58
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479342"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Specifica dell'attributo sql:inverse in sql:relationship (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  L'attributo **SQL: inverse** è utile solo quando lo schema XSD viene utilizzato per il caricamento bulk o per un updategram. L'attributo **SQL: inverse** può essere specificato nell' **\<sql:relationship>** elemento. Negli updategram la relativa logica interpreta lo schema nella determinazione delle tabelle e delle colonne aggiornate dall'operazione dell'updategram. Le relazioni padre-figlio specificate nello schema determinano l'ordine di modifica (inserimento o eliminazione) dei record.  
  
 Nel caso di uno schema XSD in cui la relazione padre-figlio viene specificata nell'ordine inverso a quello della relazione chiave primaria/chiave esterna tra le colonne del database corrispondenti, l'operazione di inserimento o eliminazione dell'updategram non riuscirà a causa della violazione della relazione chiave primaria/chiave esterna. In questi casi, l'attributo **SQL: inverse** viene specificato (**SQL: inverse = "true"**) nell' **\<sql:relationship>** elemento e la logica dell'updategram inverte l'interpretazione della relazione padre-figlio specificata nello schema.  
  
 L'attributo **SQL: inverse** accetta un valore booleano (0 = false, 1 = true). I valori possibili sono 0, 1, true e false.  
  
 Per un esempio funzionante utilizzando l'annotazione **SQL: inverse** , vedere [specifica di uno schema di mapping con annotazioni in un updategram](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione di relazioni tramite SQL: Relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
