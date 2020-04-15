---
title: 'Istruzioni UPDATE, DELETE e INSERT : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284261"
---
# <a name="update-delete-and-insert-statements"></a>Istruzioni UPDATE, DELETE e INSERT
Le applicazioni basate su SQL apportano modifiche alle tabelle eseguendo le istruzioni **UPDATE**, **DELETE**e **INSERT.** Queste istruzioni fanno parte del livello di conformità grammaticale SQL minimo e devono essere supportate da tutti i driver e le origini dati.  
  
 La sintassi di queste istruzioni è:  
  
 **UPDATE** _nome tabella_  
  
 **IDENTIFICATORe** _column-identifier_ **=** di colonna SET -*espressione* &#124; **NULL**  
  
 [**,** _identificatore_ **=** di colonna ,*espressione* &#124; **NULL...**  
  
 [**WHERE** _condizione di ricerca_]  
  
 **DELETE FROM** _nome tabella_[**WHERE** _ricerca-condizione_]  
  
 **INSERT INTO** _nome tabella_[**(** _identificatore di colonna_ [**,** _identificatore di colonna_]... **)**]  
  
 -*query-specific&#124;* **VALUES (** _insert-value_ [**,** _insert-value_]... **)**}  
  
 Si noti che l'elemento *query-specification* è valido solo nelle grammatiche Core e SQL estese e che gli elementi *di espressione* e condizione *di ricerca* diventano più complessi nelle grammatiche Core ed Extended SQL.  
  
 Analogamente ad altre istruzioni SQL, le istruzioni **UPDATE**, **DELETE**e **INSERT** sono spesso più efficienti quando utilizzano parametri. Ad esempio, la seguente istruzione può essere preparata ed eseguita ripetutamente per inserire più righe nella tabella Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Questa efficienza può essere aumentata passando matrici di valori di parametro. Per ulteriori informazioni sui parametri di istruzione e sulle matrici di valori di parametro, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md).
