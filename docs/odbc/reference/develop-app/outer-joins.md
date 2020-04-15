---
title: Partecipanti Esterni Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282447"
---
# <a name="outer-joins"></a>Outer join
ODBC supporta la sintassi SQL-92 left, right e full outer join. La sequenza di escape per gli outer join è  
  
 **oj** _outer-join_**}**  
  
 dove *è l'outer-join*  
  
 *riferimento alla tabella* :**SINISTRA &#124; DESTRA &#124; FULL, OUTER JOIN** , riferimento alla*tabella* &#124; *outer-join*, _condizione di ricerca_ **ON**  
  
 *table-reference* specifica un nome di tabella e *search-condition* specifica la condizione di join tra i *riferimenti di tabella*.  
  
 Una richiesta outer join deve essere visualizzata dopo la parola chiave **FROM** e prima della clausola **WHERE** (se presente). Per informazioni complete sulla sintassi, vedere [Sequenza](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) di escape Join esterno nell'Appendice C: grammatica SQL.  
  
 Ad esempio, le istruzioni SQL seguenti creano lo stesso set di risultati che elenca tutti i clienti e mostra che dispone di ordini aperti. La prima istruzione utilizza la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa per Oracle e non è interoperabile.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 Per determinare i tipi di outer join supportati da un'origine dati e dal supporto dei driver, un'applicazione chiama **SQLGetInfo** con il flag di SQL_OJ_CAPABILITIES. I tipi di outer join che potrebbero essere supportati sono left, right, full o nested outer join; outer join in cui i nomi di colonna nella clausola **ON** non hanno lo stesso ordine dei rispettivi nomi di tabella nella clausola **OUTER JOIN;** inner join in combinazione con outer join; e outer join utilizzando qualsiasi operatore di confronto ODBC. Se il tipo di informazioni SQL_OJ_CAPABILITIES restituisce 0, non è supportata alcuna clausola outer join.
