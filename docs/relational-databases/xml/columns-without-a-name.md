---
title: Colonne senza nome | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d8fb8fc597fd0562640821769e3314b4f3020bb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68112899"
---
# <a name="columns-without-a-name"></a>Colonne senza nome
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Qualsiasi colonna priva di nome verrà resa inline. Le colonne calcolate o le query scalari nidificate, ad esempio, che non specificano un alias di colonna genereranno colonne senza nome. Se la colonna è di tipo **xml** , viene inserito il contenuto dell'istanza di quel tipo di dati. In caso contrario, il contenuto della colonna viene inserito come nodo di testo.  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 Produrre questo codice XML. Per impostazione predefinita, per ogni riga del set di righe viene generato un elemento <`row`> nel codice XML risultante, come avviene in modalità RAW.  
  
 `<row>4</row>`  
  
 La query seguente restituisce un set di righe a tre colonne. La terza colonna priva di nome contiene dati XML. La modalità PATH inserisce un'istanza del tipo XML.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 Risultato parziale:  
  
```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location ...LocationID="10" ...></MI:Location>
  <MI:Location ...LocationID="20" ...></MI:Location>
  ...
</row>
```

## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
