---
title: SQL incorporato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915418"
---
# <a name="embedded-sql"></a>SQL incorporato
La prima tecnica per l'invio di istruzioni SQL al sistema DBMS è Embedded SQL. Poiché SQL non usa variabili e istruzioni per il controllo di flusso, viene spesso usato come sottolingua del database che può essere aggiunto a un programma scritto in un linguaggio di programmazione convenzionale, ad esempio C o COBOL. Si tratta di un'idea centrale di SQL embedded: inserire istruzioni SQL in un programma scritto in un linguaggio di programmazione host. In breve, le tecniche seguenti vengono usate per incorporare le istruzioni SQL in un linguaggio host:  
  
-   Le istruzioni SQL incorporate vengono elaborate da un precompilatore SQL speciale. Tutte le istruzioni SQL iniziano con un introduttore e terminano con un carattere di terminazione, entrambe le quali contrassegnano l'istruzione SQL per il precompilatore. L'introduttore e il terminatore variano a seconda del linguaggio host. Ad esempio, l'introduttore è "EXEC SQL" in C e "&SQL (" in parotite e il carattere di terminazione è un punto e virgola (;) in C e una parentesi destra in parotite.  
  
-   Le variabili del programma applicativo, denominate variabili host, possono essere usate nelle istruzioni SQL incorporate laddove sono consentite costanti. Questi possono essere usati nell'input per adattare un'istruzione SQL a una situazione specifica e nell'output per ricevere i risultati di una query.  
  
-   Le query che restituiscono una singola riga di dati vengono gestite con un'istruzione SELECT singleton; Questa istruzione specifica sia la query che le variabili host in cui restituire i dati.  
  
-   Le query che restituiscono più righe di dati vengono gestite con cursori. Un cursore tiene traccia della riga corrente all'interno di un set di risultati. L'istruzione DECLARE CURSOR definisce la query, l'istruzione OPEN avvia l'elaborazione della query, l'istruzione FETCH recupera le righe di dati successive e l'istruzione CLOSE termina l'elaborazione della query.  
  
-   Mentre un cursore è aperto, è possibile utilizzare le istruzioni di eliminazione posizionate e di aggiornamento posizionate per aggiornare o eliminare la riga attualmente selezionata dal cursore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esempio di SQL incorporato](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilazione di un programma Embedded SQL](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL statico](../../odbc/reference/static-sql.md)  
  
-   [SQL dinamica](../../odbc/reference/dynamic-sql.md)
