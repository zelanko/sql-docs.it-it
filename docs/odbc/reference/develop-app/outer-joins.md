---
title: Outer join | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4bf875b3afd21f6b8cb211c999401b0ecb80879
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987819"
---
# <a name="outer-joins"></a>Outer join
ODBC supporta la sintassi di SQL-92 left, Right e full outer join. La sequenza di escape per outer join è  
  
 **{GU** _outer join_**}**  
  
 dove *outer join* è  
  
 *Table-Reference* {**LEFT &#124; right &#124; full} outer join** {*Table-Reference* &#124; *outer-join*} **nella condizione di** _ricerca_  
  
 *Table-Reference* specifica un nome di tabella e la *condizione di ricerca* specifica la condizione di join tra i riferimenti a *tabella*.  
  
 Una richiesta outer join deve comparire dopo la parola chiave **from** e prima della clausola **where** (se presente). Per informazioni complete sulla sintassi, vedere [sequenza di escape outer join](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) nell'Appendice C: grammatica SQL.  
  
 Le istruzioni SQL seguenti, ad esempio, creano lo stesso set di risultati che elenca tutti i clienti e Mostra gli ordini aperti. La prima istruzione usa la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa per Oracle e non è interoperativa.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Per determinare i tipi di outer join supportati da un'origine dati e da un driver, un'applicazione chiama **SQLGetInfo** con il flag SQL_OJ_CAPABILITIES. I tipi di outer join che potrebbero essere supportati sono Left, right, Full o Nested outer join; outer join in cui i nomi di colonna nella clausola **on** non hanno lo stesso ordine dei rispettivi nomi di tabella nella clausola **outer join** . Inner join insieme a outer join; e outer join utilizzando qualsiasi operatore di confronto ODBC. Se il tipo di informazioni SQL_OJ_CAPABILITIES restituisce 0, non è supportata alcuna clausola outer join.
