---
title: Colonne con il nome di un test di nodo XPath | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
- XPath node test
ms.assetid: b48adccd-3b6b-486a-b326-20f57170186f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 804ca2ebe3aa307272645fa5a626ea2212367f87
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530853"
---
# <a name="columns-with-the-name-of-an-xpath-node-test"></a>Colonne con il nome di un test di nodo XPath
  Se il nome della colonna è uno dei test di nodo XPath, il mapping del contenuto viene eseguito come illustrato nella tabella seguente. Quando il nome della colonna è un test di nodo XPath, il mapping viene eseguito tra il contenuto e il nodo corrispondente. Se il tipo SQL della colonna è `xml`, viene generato un errore.  
  
|Nome colonna|Comportamento|  
|-----------------|--------------|  
|text()|Per una colonna con nome text(), il valore stringa contenuto nella colonna viene aggiunto come nodo di testo.|  
|comment()|Per una colonna con nome comment(), il valore stringa contenuto nella colonna viene aggiunto come commento XML.|  
|node()|Per una colonna con nome node(), il risultato è lo stesso di quando il nome della colonna è un carattere jolly (*).|  
|processing-instruction(name)|Per una colonna il cui nome corrisponde a quello di un'istruzione di elaborazione, il valore stringa contenuto nella colonna viene aggiunto come valore PI per il nome di destinazione dell'istruzione di elaborazione.|  
  
 Nella query seguente viene illustrato l'utilizzo dei test di nodo come nomi di colonna. I nodi di testo e i commenti vengono aggiunti nel codice XML risultante.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
        'Example of using node tests such as text(), comment(), processing-instruction()'                as "comment()",  
        'Some PI'                   as "processing-instruction(PI)",  
        'Employee name and address data' as "text()",  
        'middle name is optional'        as "EmpName/text()",  
        FirstName                        as "EmpName/First",   
        MiddleName                       as "EmpName/Middle",   
        LastName                         as "EmpName/Last",  
        AddressLine1                     as "Address/AddrLine1",  
        AddressLine2                     as "Address/AddrLIne2",  
        City                             as "Address/City"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P   
    ON P.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS BAE  
    ON BAE.BusinessEntityID = E.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BAE.AddressID = A.AddressID  
WHERE  E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Questo è il risultato:  
  
 `<row EmpID="1">`  
  
 `<!--Example of using node tests such as text(), comment(), processing-instruction() -->`  
  
 `<?PI Some PI?>`  
  
 `Employee name and address data`  
  
 `<EmpName>middle name is optional`  
  
 `<First>Ken</First>`  
  
 `<Last>S??nchez</Last>`  
  
 `</EmpName>`  
  
 `<Address>`  
  
 `<AddrLine1>4350 Minute Dr.</AddrLine1>`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</row>`  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
