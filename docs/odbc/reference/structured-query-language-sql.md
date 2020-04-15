---
title: Linguaggio di query strutturato (SQL) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293391"
---
# <a name="structured-query-language-sql"></a>Structured Query Language (SQL)
Un tipico DBMS consente agli utenti di archiviare, accedere e modificare i dati in modo organizzato ed efficiente. Originariamente, gli utenti di DBMS erano programmatori. L'accesso ai dati memorizzati richiedeva la scrittura di un programma in un linguaggio di programmazione come COBOL. Mentre questi programmi sono stati spesso scritti per presentare un'interfaccia amichevole a un utente non tecnico, l'accesso ai dati stessi richiedeva i servizi di un programmatore esperto. L'accesso occasionale ai dati non era pratico.  
  
 Gli utenti non erano del tutto soddisfatti di questa situazione. Mentre potevano accedere ai dati, spesso richiedeva convincere un programmatore DBMS a scrivere un software speciale. Ad esempio, se un reparto vendite desiderava visualizzare le vendite totali del mese precedente da parte di ciascuno dei suoi venditori e desiderava che queste informazioni fossero ordinate in base alla durata del servizio di ciascun venditore nell'azienda, aveva due scelte: o esisteva già un programma che consentiva l'accesso alle informazioni esattamente in questo modo, oppure il reparto doveva chiedere a un programmatore di scrivere un programma di questo tipo. In molti casi, questo è stato più lavoro di quanto valesse, ed era sempre una soluzione costosa per le richieste una tantanche o ad hoc. Come sempre più utenti volevano un facile accesso, questo problema è cresciuto sempre più grande.  
  
 Consentire agli utenti di accedere ai dati su base ad hoc richiedeva di fornire loro un linguaggio in cui esprimere le loro richieste. Una singola richiesta a un database è definita come una query. tale linguaggio è chiamato linguaggio di query. Molti linguaggi di query sono stati sviluppati per questo scopo, ma uno di questi è diventato il più popolare: Structured Query Language, inventato da IBM nel 1970. È più comunemente conosciuto con il suo acronimo, SQL, ed è pronunciato sia come "ess-cue-ell" che come "sequel". SQL è diventato uno standard ANSI nel 1986 e uno standard ISO nel 1987; viene utilizzato oggi in un gran numero di sistemi di gestione di database.  
  
 Anche se SQL ha risolto le esigenze ad hoc degli utenti, la necessità di accesso ai dati da parte di programmi per computer non è andata via. Infatti, la maggior parte dell'accesso al database era (ed è) programmatico, sotto forma di report regolarmente programmati e analisi statistiche, programmi di immissione dati come quelli utilizzati per l'immissione degli ordini e programmi di manipolazione dei dati, come quelli utilizzati per riconciliare i conti e generare ordini di lavoro.  
  
 Questi programmi utilizzano anche SQL, utilizzando una delle tre tecniche seguenti:  
  
-   **Embedded SQL**, in cui le istruzioni SQL sono incorporate in un linguaggio host, ad esempio C o COBOL.  
  
-   **Moduli SQL**, in cui le istruzioni SQL vengono compilate nel sistema DBMS e chiamate da un linguaggio host.  
  
-   **Interfaccia**a livello di chiamata , o CLI, costituita da funzioni chiamate per passare istruzioni SQL al DBMS e recuperare i risultati dal DBMS.  
  
> [!NOTE]  
>  Si tratta di un incidente storico che il termine interfaccia a livello di chiamata viene utilizzato al posto dell'API (Application Programming Interface), un altro termine per la stessa cosa. Nel mondo del database, l'API viene usata per descrivere SQL stesso: SQL è l'API di un DBMS.  
  
 Di queste scelte, SQL incorporato è il più comunemente usato, anche se la maggior parte dei principali DBSMO supporta cLIs proprietari.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elaborazione di un'istruzione SQLProcessing an SQL Statement](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [Embedded SQL](../../odbc/reference/embedded-sql.md)  
  
-   [Moduli SQL](../../odbc/reference/sql-modules.md)  
  
-   [Call-Level Interface](../../odbc/reference/call-level-interfaces.md)
