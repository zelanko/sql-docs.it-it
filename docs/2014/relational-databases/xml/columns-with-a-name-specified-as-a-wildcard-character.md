---
title: Colonne con nome specificato come carattere jolly | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 899ea4a4f60fb3e8981de4119697864a24f57093
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362799"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Colonne con nome specificato come carattere jolly
  Se il nome di colonna specificato è un carattere jolly (\*), il contenuto della colonna viene inserito come se non fosse stato specificato alcun nome di colonna. Se la colonna non è di tipo `xml`, il relativo contenuto viene inserito come nodo di testo, come illustrato nell'esempio seguente:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Questo è il risultato:  
  
 `<row EmpID="1">KenJS??nchez</row>`  
  
 Se la colonna è di tipo `xml`, viene inserito l'albero XML corrispondente. Ad esempio, la query seguente specifica "*" come nome della colonna che contiene il codice XML restituito dall'espressione XQuery eseguita sulla colonna Instructions.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 Di seguito è riportato il risultato. Il codice XML restituito dalla XQuery viene inserito senza un elemento di wrapping.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
