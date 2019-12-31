---
title: Memorizzazione nella cache degli schemi (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32a825f4cfc0a90ce9cba879b6b64856effabe6d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257308"
---
# <a name="schema-caching-sqlxml-40"></a>Memorizzazione nella cache degli schemi (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Con un'installazione side-by-side di XML per Microsoft SQL Server 2000 Web Release 1, Microsoft SQLXML 2.0 e SQLXML 3.0, è possibile controllare in modo esplicito la memorizzazione degli schemi nella cache in tutte le versioni attraverso le chiavi del Registro di sistema seguenti:  
  
 Web Release 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2,0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Per ulteriori informazioni sull'installazione side-by-Side, vedere Novità [di SQLXML 4,0 SP1](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 La memorizzazione nella cache degli schemi migliora notevolmente le prestazioni di una query XPath. Quando una query XPath viene eseguita su uno schema di mapping, lo schema viene archiviato in memoria e le strutture dei dati necessarie vengono incluse in memoria. Se la memorizzazione nella cache degli schemi è impostata, lo schema resta in memoria e comporta un miglioramento delle prestazioni per le query XPath successive.  
  
 È possibile impostare le dimensioni della cache degli schemi aggiungendo nel Registro di sistema la chiave sopra riportata.  
  
 Le dimensioni dello schema vengono impostate in base sulla memoria disponibile e al numero di schemi utilizzati. Le dimensioni predefinite di **SchemaCacheSize** sono 31. Se si imposta **SchemaCacheSize** su un valore superiore, viene utilizzata una quantità maggiore di memoria. Pertanto, è possibile aumentare le dimensioni della cache se l'accesso allo schema sembra lento o ridurle se la memoria è insufficiente.  
  
 Per motivi di prestazioni, è consigliabile impostare **SchemaCacheSize** su un valore superiore al numero di schemi di mapping utilizzati in genere. Con l'aumentare del numero di schemi, se **SchemaCacheSize** è inferiore al numero di schemi disponibili, le prestazioni diminuiscono.  
  
> [!NOTE]  
>  Durante lo sviluppo, è consigliabile non memorizzare nella cache gli schemi, in quanto le modifiche apportate agli schemi non vengono riflesse nella cache per circa due minuti.  
  
## <a name="see-also"></a>Vedere anche  
 [Caching del modello &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Caching XSL &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
