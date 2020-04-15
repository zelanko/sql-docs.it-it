---
title: 'SQL incorporato : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306674"
---
# <a name="embedded-sql"></a>SQL incorporato
La prima tecnica per l'invio di istruzioni SQL al DBMS è SQL incorporato. Poiché SQL non utilizza variabili e istruzioni di controllo del flusso, viene spesso utilizzato come sottolinguaggio di database che può essere aggiunto a un programma scritto in un linguaggio di programmazione convenzionale, ad esempio C o COBOL. Questa è un'idea centrale di SQL incorporato: inserimento di istruzioni SQL in un programma scritto in un linguaggio di programmazione host. In breve, le seguenti tecniche vengono utilizzate per incorporare istruzioni SQL in un linguaggio host:  
  
-   Le istruzioni SQL incorporate vengono elaborate da uno speciale precompilatore SQL. Tutte le istruzioni SQL iniziano con un'introduzione e terminano con un terminatore, che contrassegnano entrambe l'istruzione SQL per il precompilatore. L'introduzione e il terminatore variano in base alla lingua dell'host. Ad esempio, l'introduzione è "EXEC SQL" in C e "&SQL" in MUMPS e il terminatore è un punto e virgola (;) in C e una parentesi destra in MUMPS.  
  
-   Le variabili del programma applicativo, denominate variabili host, possono essere utilizzate nelle istruzioni SQL incorporate ovunque siano consentite costanti. Questi possono essere utilizzati sull'input per adattare un'istruzione SQL a una situazione specifica e nell'output per ricevere i risultati di una query.  
  
-   Le query che restituiscono una singola riga di dati vengono gestite con un'istruzione SELECT singleton. questa istruzione specifica sia la query che le variabili host in cui restituire i dati.  
  
-   Le query che restituiscono più righe di dati vengono gestite con i cursori. Un cursore tiene traccia della riga corrente all'interno di un set di risultati. L'istruzione DECLARE CURSOR definisce la query, l'istruzione OPEN inizia l'elaborazione della query, l'istruzione FETCH recupera righe successive di dati e l'istruzione CLOSE termina l'elaborazione della query.  
  
-   Mentre un cursore è aperto, le istruzioni di aggiornamento posizionato e di eliminazione posizionate possono essere utilizzate per aggiornare o eliminare la riga attualmente selezionata dal cursore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esempio di Embedded SQL](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilazione di un programma Embedded SQL](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL statico](../../odbc/reference/static-sql.md)  
  
-   [SQL dinamica](../../odbc/reference/dynamic-sql.md)
