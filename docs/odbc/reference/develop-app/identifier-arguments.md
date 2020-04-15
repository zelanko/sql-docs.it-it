---
title: Argomenti dell'identificatore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300161"
---
# <a name="identifier-arguments"></a>Argomenti di tipo identificatore
Se una stringa in un identificatore argomento è racchiusa tra virgolette, il driver rimuove gli spazi vuoti iniziali e finali e considera letteralmente la stringa all'interno delle virgolette. Se la stringa non è racchiusa tra virgolette, il driver rimuove gli spazi vuoti finali e piega la stringa in maiuscolo. L'impostazione di un argomento identificatore su un puntatore null restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null), a meno che l'argomento non sia un nome di catalogo e i cataloghi non siano supportati.  
  
 Questi argomenti vengono considerati come argomenti di tipo identificatore se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE. In questo caso, il trattino di sottolineatura (_) e il segno di percentuale (%) verrà considerato come il carattere effettivo, non come un carattere del criterio di ricerca. Questi argomenti vengono considerati come un argomento ordinario o un argomento di modello, a seconda dell'argomento, se questo attributo è impostato su SQL_FALSE.  
  
 Anche se gli identificatori contenenti caratteri speciali devono essere racchiusi tra virgolette nelle istruzioni SQL, non devono essere racchiusi tra virgolette quando vengono passati come argomenti della funzione di catalogo, perché i caratteri virgolette passati alle funzioni di catalogo vengono interpretati letteralmente. Si supponga, ad esempio, che il carattere di virgoletta dell'identificatore (specifico del driver e restituito tramite **SQLGetInfo**) sia una virgoletta doppia ("). La prima chiamata a **SQLTables** restituisce un set di risultati contenente informazioni sulla tabella Contabilità fornitori, mentre la seconda chiamata restituisce informazioni sulla tabella "Contabilità fornitori", che probabilmente non è quella prevista.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Gli identificatori tra virgolette vengono utilizzati per distinguere un nome di colonna true da una pseudo-colonna con lo stesso nome, ad esempio ROWID in Oracle.Quoted identifiers are used to distinguish a true column name from a pseudo-column of the same name, such as ROWID in Oracle. Se "ROWID" viene passato in un argomento di una funzione di catalogo, la funzione funzionerà con la pseudo-colonna ROWID se esistente. Se la pseudo-colonna non esiste, la funzione funzionerà con la colonna "ROWID". Se ROWID viene passato in un argomento di una funzione di catalogo, la funzione funzionerà con la colonna ROWID.  
  
 Per ulteriori informazioni sugli identificatori tra virgolette, vedere [Identificatori tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).
