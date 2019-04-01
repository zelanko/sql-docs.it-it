---
title: Convertire colonne esistenti in colonne XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca7aff5e3b0383f8db5f5c2f45027f3e00cefc20
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510518"
---
# <a name="change-existing-columns-to-xml-columns"></a>Conversione di colonne esistenti a colonne XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  L'istruzione ALTER TABLE supporta il tipo di dati **xml** . Ad esempio, è possibile modificare qualsiasi colonna di tipo string nel tipo di dati **xml** . Si noti che in questi casi è necessaria la correttezza del formato dei documenti contenuti nella colonna. Se inoltre si sta modificando il tipo della colonna da stringa a XML tipizzato, i documenti nella colonna vengono convalidati rispetto agli schemi XSD specificati.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max))  
GO  
INSERT INTO T   
VALUES (1, '<Root><Product ProductID="1"/></Root>')  
GO  
ALTER TABLE T   
ALTER COLUMN Col2 xml  
GO  
```  
  
 È possibile modificare una colonna di tipo `xml` da XML non tipizzato a XML tipizzato. Esempio:  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T   
values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>')  
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection)  
GO  
```  
  
> [!NOTE]  
>  Lo script verrà eseguito sul database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , poiché la raccolta XML Schema `Production.ProductDescriptionSchemaCollection`viene creata come parte del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 Nell'esempio precedente, tutte le istanze archiviate nella colonna vengono convalidate e tipizzate rispetto agli schemi XSD nella raccolta specificata. Se la colonna contiene una o più istanze XML non valide rispetto allo schema specificato, l'istruzione `ALTER TABLE` avrà esito negativo e non sarà possibile modificare il tipo della colonna da XML non tipizzato a XML tipizzato.  
  
> [!NOTE]  
>  Se una tabella è di grandi dimensioni, la modifica di una colonna di tipo **xml** può risultare onerosa, poiché è necessario un controllo di correttezza del formato di ogni documento e, nel caso del codice XML tipizzato, è necessaria anche la convalida.  
  
 Per altre informazioni sul codice XML tipizzato, vedere [Confrontare dati XML tipizzati con dati XML non tipizzati](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
  
