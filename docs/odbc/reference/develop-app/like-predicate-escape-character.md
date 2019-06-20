---
title: COME carattere di Escape nel predicato | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 30547551cc1793622eaa981c07bbc002d07a094d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312914"
---
# <a name="like-predicate-escape-character"></a>Carattere di escape nel predicato LIKE
In un **, ad esempio** predicato, il segno di percentuale (%) corrisponde a zero o più di qualsiasi carattere e il carattere di sottolineatura (_) corrisponde a qualsiasi carattere. In base a un segno di percentuale effettivo o un carattere di sottolineatura un **, ad esempio** predicato, un carattere di escape deve precedere il segno di percentuale o un carattere di sottolineatura. La sequenza di escape che definisce il **, ad esempio** carattere di escape nel predicato è:  
  
 **{escape '** *carattere di escape* **'}**  
  
 in cui *carattere di escape* è qualsiasi carattere supportati dall'origine dati.  
  
 Per altre informazioni su questo tipo di sequenza di escape, vedere [come sequenza di Escape](../../../odbc/reference/appendixes/like-escape-sequence.md) nell'appendice c: Grammatica SQL.  
  
 Le istruzioni SQL seguenti, ad esempio, creano lo stesso set di risultati del cliente nomi che iniziano con i caratteri "% AAA". La prima istruzione Usa la sintassi di escape-sequence. La seconda istruzione viene utilizzata la sintassi nativa per Microsoft® Access e non è interoperativa. Si noti che la percentuale secondo carattere in ognuno **, ad esempio** predicato è un carattere jolly che corrisponde a zero o più di qualsiasi carattere.  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 Per determinare se il **, ad esempio** caratteri di escape nel predicato sono supportata da un'origine dati, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_LIKE_ESCAPE_CLAUSE.
