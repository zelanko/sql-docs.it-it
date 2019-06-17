---
title: Argomenti di tipo identificatore | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447550"
---
# <a name="identifier-arguments"></a>Argomenti di tipo identificatore
Se una stringa in un argomento dell'identificatore sia racchiusa tra virgolette, il driver rimuove iniziali e gli spazi vuoti finali e letteralmente considera la stringa tra virgolette. Se la stringa non è racchiuso tra virgolette, il driver rimuove riduzioni e gli spazi vuoti finali stringa in maiuscolo. L'impostazione di un argomento dell'identificatore a un puntatore null restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null), a meno che l'argomento è un nome di catalogo e i cataloghi non sono supportati.  
  
 Se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_TRUE, questi argomenti vengono trattati come argomenti di tipo identificatore. In questo caso, il carattere di sottolineatura (_) e la percentuale di accedere (%) viene considerato come il carattere effettivo, non come un carattere di pattern di ricerca. Questi argomenti vengono trattati come un normale argomento o un argomento di modello, a seconda dell'argomento, se questo attributo è impostato su SQL_FALSE.  
  
 Anche se gli identificatori che contengono caratteri speciali devono essere racchiusi tra virgolette in istruzioni SQL, è necessario non essere racchiusi tra virgolette quando vengono passati come argomenti della funzione di catalogo, poiché le virgolette passate alle funzioni di catalogo vengono interpretate letteralmente. Si supponga ad esempio l'identificatore del tipo di virgolette (che è specifico del driver e viene restituita tramite **SQLGetInfo**) è un segno di virgolette doppie ("). La prima chiamata a **SQLTables** restituisce un set di risultati contenente informazioni sulla tabella di contabilità, mentre la seconda chiamata restituisce informazioni sulla tabella "Contabilità fornitori", che è probabile che non era previsto.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Gli identificatori delimitati vengono utilizzati per distinguere un nome di colonna true da una pseudo colonna lo stesso nome, ad esempio ROWID in Oracle. Se "ROWID" viene passato un argomento di una funzione di catalogo, la funzione funzionerà con la pseudo-colonna di ROWID se esistente. Se la pseudo-colonna non esiste, la funzione funzionerà con la colonna "ROWID". Se ROWID viene passato un argomento di una funzione di catalogo, la funzione funzionerà con la colonna ROWID.  
  
 Per altre informazioni sugli identificatori tra virgolette, vedere [identificatori racchiusi tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).
