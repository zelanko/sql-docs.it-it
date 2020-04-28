---
title: Argomenti identificatore | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300161"
---
# <a name="identifier-arguments"></a>Argomenti di tipo identificatore
Se una stringa in un argomento identificatore è racchiusa tra virgolette, il driver rimuove gli spazi vuoti iniziali e finali e gestisce letteralmente la stringa racchiusa tra virgolette. Se la stringa non è racchiusa tra virgolette, il driver rimuove gli spazi vuoti finali e la stringa in maiuscolo. L'impostazione di un argomento identificatore su un puntatore null restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null), a meno che l'argomento non sia un nome di catalogo e i cataloghi non sono supportati.  
  
 Questi argomenti vengono trattati come argomenti identificatore se l'attributo SQL_ATTR_METADATA_ID istruzione è impostato su SQL_TRUE. In questo caso, il carattere di sottolineatura (_) e il segno di percentuale (%) verrà considerato come il carattere effettivo, non come un carattere di ricerca. Questi argomenti vengono trattati come un argomento ordinario o un argomento di modello, a seconda dell'argomento, se questo attributo è impostato su SQL_FALSE.  
  
 Sebbene gli identificatori contenenti caratteri speciali debbano essere racchiusi tra virgolette in istruzioni SQL, non devono essere racchiusi tra virgolette quando vengono passati come argomenti della funzione di catalogo, perché i caratteri virgoletta passati alle funzioni di catalogo vengono interpretati letteralmente. Si supponga, ad esempio, che il carattere virgoletta identificatore, che è specifico del driver e restituito tramite **SQLGetInfo**, sia racchiuso tra virgolette doppie ("). La prima chiamata a **SQLTables** restituisce un set di risultati contenente informazioni sulla tabella degli account pagabili, mentre la seconda chiamata restituisce informazioni sulla tabella "Accounts pagabile", che probabilmente non è stata progettata.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Gli identificatori delimitati vengono utilizzati per distinguere un nome di colonna reale da una pseudo-colonna con lo stesso nome, ad esempio ROWID in Oracle. Se "ROWID" viene passato in un argomento di una funzione di catalogo, la funzione funzionerà con la pseudo-colonna ROWID se esiste. Se la pseudo-colonna non esiste, la funzione funzionerà con la colonna "ROWID". Se ROWID viene passato in un argomento di una funzione di catalogo, la funzione funziona con la colonna ROWID.  
  
 Per ulteriori informazioni sugli identificatori delimitati, vedere [identificatori delimitati](../../../odbc/reference/develop-app/quoted-identifiers.md).
