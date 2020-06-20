---
title: 'Esempio: specifica della direttiva ELEMENTXSINIL | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
author: rothja
ms.author: jroth
ms.openlocfilehash: 381f93f5c8bd5df0dc37a1f0b511aff0c830f013
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067801"
---
# <a name="example-specifying-the-elementxsinil-directive"></a>Esempio: specifica della direttiva ELEMENTXSINIL
  Quando si specifica la direttiva ELEMENT per il recupero di codice XML incentrato sugli elementi, se la colonna contiene un valore NULL, l'elemento corrispondente non viene generato nella modalità EXPLICIT. È possibile specificare facoltativamente la direttiva ELEMENTXSINIL per richiedere la creazione dell'elemento per i valori NULL. In questo caso l'attributo `xsi:nil` viene impostato sul valore TRUE.  
  
 La query seguente genera codice XML che include l'indirizzo di un dipendente. Per le colonne `AddressLine2` e `City` i nomi di colonna specificano la direttiva `ELEMENTXSINIL` . Ciò comporta la generazione dell'elemento per i valori NULL nelle colonne `AddressLine2` e `City` del set di righe.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 Risultato parziale:  
  
 `<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `EmpID="1" AddressID="249">`  
  
 `<Address AddressID="249">`  
  
 `<AddressLine1>4350 Minute Dr.</AddressLine1>`  
  
 `<AddressLine2 xsi:nil="true" />`  
  
 `<City>Minneapolis</City>`  
  
 `</Address>`  
  
 `</Employee>`  
  
 `...`  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
