---
title: Carattere di escape del predicato LIKE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20310c60759aea17d61b9252fd73d226567a7a54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68027236"
---
# <a name="like-predicate-escape-character"></a>Carattere di escape nel predicato LIKE
In un predicato **like** , il segno di percentuale (%) trova la corrispondenza di zero o più caratteri e il carattere di sottolineatura (_) corrisponde a un qualsiasi carattere. Per trovare la corrispondenza con un segno di percentuale effettivo o un carattere di sottolineatura in un predicato **like** , un carattere di escape deve precedere il segno di percentuale o il carattere La sequenza di escape che definisce il carattere di escape del predicato **like** è:  
  
 **{escape '** *carattere di escape* **'}**  
  
 dove *Escape-Character* è qualsiasi carattere supportato dall'origine dati.  
  
 Per ulteriori informazioni sulla sequenza di escape LIKE, vedere [like escape sequence](../../../odbc/reference/appendixes/like-escape-sequence.md) in Appendice C: grammatica SQL.  
  
 Ad esempio, le istruzioni SQL seguenti creano lo stesso set di risultati dei nomi dei clienti che iniziano con i caratteri "% AAA". La prima istruzione usa la sintassi della sequenza di escape. La seconda istruzione usa la sintassi nativa per Microsoft® Access e non è interoperativa. Si noti che il secondo carattere di percentuale in ogni predicato **like** è un carattere jolly che corrisponde a zero o più caratteri.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Per determinare se il carattere di escape del predicato **like** è supportato da un'origine dati, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_LIKE_ESCAPE_CLAUSE.
