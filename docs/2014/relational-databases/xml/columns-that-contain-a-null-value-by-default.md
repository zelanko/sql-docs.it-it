---
title: Colonne contenenti un valore NULL per impostazione predefinita | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c98e5cf869b0a4b7e39b640cf4f486ae8f222127
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637751"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Colonne contenenti un valore NULL per impostazione predefinita
  Per impostazione predefinita, la presenza di un valore Null in una colonna corrisponde all'assenza dell'attributo, nodo o elemento. Questo funzionamento predefinito può essere sovrascritto richiedendo un valore XML incentrato sugli elementi mediante la direttiva ELEMENTS e specificando XSINIL per richiedere l'aggiunta di elementi per i valori NULL, come illustrato nella query seguente:  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 Il risultato è illustrato di seguito. Non specificando XSINIL, l'elemento <`Middle`> non sarà presente.  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzare la modalità PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
