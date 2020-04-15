---
title: Carattere di escape del predicato di LIKE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e4f04b12911145eede3354532736cb92f1ae413
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306152"
---
# <a name="like-predicate-escape-character"></a>Carattere di escape nel predicato LIKE
In un predicato **LIKE,** il segno di percentuale (%) corrisponde a zero o più caratteri e il carattere di sottolineatura (_) corrisponde a qualsiasi carattere. Per trovare una corrispondenza con un segno di percentuale o un carattere di sottolineatura effettivo in un predicato **LIKE,** un carattere di escape deve precedere il segno di percentuale o il carattere di sottolineatura. La sequenza di escape che definisce il carattere di escape del predicato **LIKE** è:  
  
 **' carattere** *di escape* **'**  
  
 dove *carattere di escape* è qualsiasi carattere supportato dall'origine dati.  
  
 Per altre informazioni sulla sequenza di escape LIKE, vedere [Sequenza](../../../odbc/reference/appendixes/like-escape-sequence.md) di escape LIKE nell'Appendice C: Grammatica SQL.  
  
 Ad esempio, le istruzioni SQL seguenti creano lo stesso set di risultati di nomi di clienti che iniziano con i caratteri "%AAA". La prima istruzione utilizza la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa per Microsoft® Access e non è interoperabile. Si noti che il secondo carattere percentuale in ogni predicato **LIKE** è un carattere jolly che corrisponde a zero o più di qualsiasi carattere.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Per determinare se il carattere di escape del predicato **LIKE** è supportato da un'origine dati, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_LIKE_ESCAPE_CLAUSE.
