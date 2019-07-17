---
title: Embedded SQL | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915418"
---
# <a name="embedded-sql"></a>SQL incorporato
La prima tecnica per l'invio di istruzioni SQL per il sistema DBMS è incorporata SQL. Poiché SQL non usa le variabili e le istruzioni di controllo di flusso, viene spesso utilizzato come un sottolinguaggio per i database che può essere aggiunti a un programma scritto in un linguaggio di programmazione convenzionale, ad esempio C o COBOL. Si tratta di un'idea di embedded SQL centrale: posizionamento delle istruzioni SQL in un programma scritto in un host di linguaggio di programmazione. In breve, le tecniche seguenti vengono usate per incorporare le istruzioni SQL in un linguaggio host:  
  
-   Istruzioni SQL incorporate vengono elaborate da un speciale precompilatore SQL. Tutte le istruzioni SQL iniziano con un elemento introduttivo e terminano con un carattere di terminazione, che contrassegna l'istruzione SQL per il precompilatore. L'elemento introduttivo e un carattere di terminazione variano in base al linguaggio host. Ad esempio, l'elemento introduttivo è "EXEC SQL" in C e "& SQL (" agli ORECCHIONI, e il carattere di terminazione è un punto e virgola (;) in C e una parentesi chiusa agli ORECCHIONI.  
  
-   Variabili del programma dell'applicazione, chiamato le variabili di host, possono essere utilizzate nelle istruzioni SQL incorporate ogni volta che le costanti sono consentite. Possono essere usati nell'input per adattare un'istruzione SQL per una determinata situazione e sull'output che riceverà i risultati di una query.  
  
-   Le query che restituiscono una singola riga di dati vengono gestite con un'istruzione SELECT singleton. Questa istruzione specifica che la query sia le variabili di host in cui restituire i dati.  
  
-   Le query che restituiscono più righe di dati vengono gestite con i cursori. Un cursore tiene traccia di riga corrente all'interno di un set di risultati. L'istruzione DECLARE CURSOR definisce la query, l'istruzione OPEN inizia l'elaborazione delle query, l'istruzione FETCH recupera le righe successive dei dati e l'istruzione CLOSE termina l'elaborazione delle query.  
  
-   Quando un cursore è aperto, le istruzioni delete posizionate e aggiornamento posizionato utilizzabile per aggiornare o eliminare la riga attualmente selezionata dal cursore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esempio di Embedded SQL](../../odbc/reference/embedded-sql-example.md)  
  
-   [Compilazione di un programma Embedded SQL](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [SQL statico](../../odbc/reference/static-sql.md)  
  
-   [SQL dinamico](../../odbc/reference/dynamic-sql.md)
