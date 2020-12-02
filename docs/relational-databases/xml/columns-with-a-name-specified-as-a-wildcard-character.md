---
title: Specificare una colonna con un carattere jolly (SQLXML) | Microsoft Docs
description: Informazioni sul modo in cui i nomi di colonna specificati come caratteri jolly influiscono sui risultati di una query XQuery.
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 915bd2824f6e3a706587769413c0f116df859f06
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125024"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Colonne con nome specificato come carattere jolly

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Se il nome di colonna specificato è un carattere jolly (\*), il contenuto della colonna viene inserito come se non fosse stato specificato alcun nome di colonna. Se la colonna non è di tipo diverso da **xml** , il relativo contenuto viene inserito come nodo di testo, come illustrato nell'esempio seguente:  
  
```sql
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
  
 Risultato:  

```xml
<row EmpID="1">KenJSánchez</row>
```

 Se la colonna è di tipo **xml** , viene inserito l'albero XML corrispondente. Ad esempio, la query seguente specifica "*" come nome della colonna che contiene il codice XML restituito dall'espressione XQuery eseguita sulla colonna Instructions.  
  
```sql
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
```  
  
 Di seguito è riportato il risultato. Il codice XML restituito dalla XQuery viene inserito senza un elemento di wrapping.  

```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location LocationID="10">...</MI:Location>
  <MI:Location LocationID="20">...</MI:Location>
  ...
</row>
```

## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
