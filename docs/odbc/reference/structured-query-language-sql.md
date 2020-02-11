---
title: Structured Query Language (SQL) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6cae344e97bf6e5dc8affbf164f80eb8935846e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019034"
---
# <a name="structured-query-language-sql"></a>Structured Query Language (SQL)
Un DBMS tipico consente agli utenti di archiviare, accedere e modificare i dati in modo organizzato ed efficiente. In origine, gli utenti dei sistemi DBMS erano programmatori. Per accedere ai dati archiviati è necessario scrivere un programma in un linguaggio di programmazione, ad esempio COBOL. Sebbene questi programmi fossero spesso scritti per presentare un'interfaccia intuitiva a un utente non tecnico, l'accesso ai dati stessi richiedeva i servizi di un programmatore esperto. L'accesso informale ai dati non è pratico.  
  
 Gli utenti non erano completamente soddisfatti di questa situazione. Sebbene possano accedere ai dati, spesso è necessario convincere un programmatore DBMS a scrivere software speciale. Se, ad esempio, un reparto vendite voleva visualizzare le vendite totali del mese precedente da ognuno dei venditori e voleva che queste informazioni fossero classificate in base alla lunghezza del servizio di ogni venditore nell'azienda, era possibile scegliere tra due opzioni: un programma già esistente è stato consentito l'accesso alle informazioni esattamente in questo modo oppure il reparto doveva richiedere a un programmatore di scrivere un programma di questo tipo. In molti casi, si trattava di una soluzione più complessa rispetto a quella che valeva, ed era sempre una soluzione costosa per le richieste monouso o ad hoc. Poiché un numero sempre maggiore di utenti desiderava un accesso facile, questo problema cresceva e più grande.  
  
 Consentire agli utenti di accedere ai dati in base ad hoc è necessario assegnare loro un linguaggio per esprimere le proprie richieste. Una singola richiesta a un database è definita come una query; un linguaggio di questo tipo è denominato linguaggio di query. Molti linguaggi di query sono stati sviluppati a questo scopo, ma uno di questi è diventato il più diffuso: Structured Query Language, inventato presso IBM negli anni settanta. È più comunemente noto dal relativo acronimo, SQL ed è pronunciato sia come "ESS-cue-ell" sia come "sequel". SQL è diventato uno standard ANSI in 1986 e uno standard ISO in 1987; Attualmente viene usato in numerosi sistemi di gestione di database.  
  
 Sebbene SQL abbia risolto le esigenze ad hoc degli utenti, la necessità di accesso ai dati da parte dei programmi computer non è stata eliminata. Infatti, la maggior parte dell'accesso al database è ancora (e è) a livello di codice, sotto forma di report pianificati regolarmente e analisi statistiche, programmi di immissione dati come quelli usati per l'immissione dell'ordine e programmi di manipolazione dei dati, ad esempio quelli usati per riconciliare gli account e genera ordini di lavoro.  
  
 Questi programmi usano anche SQL, usando una delle tre tecniche seguenti:  
  
-   **SQL incorporato**, in cui le istruzioni SQL sono incorporate in un linguaggio host, ad esempio C o COBOL.  
  
-   **Moduli SQL**, in cui le istruzioni SQL vengono compilate nel sistema DBMS e chiamate da un linguaggio host.  
  
-   **Interfaccia a livello di chiamata**, o CLI, che è costituita da funzioni chiamate per passare istruzioni SQL al sistema DBMS e recuperare i risultati dal sistema DBMS.  
  
> [!NOTE]  
>  Si tratta di un errore storico che viene usato il termine interfaccia a livello di chiamata invece di Application Programming Interface (API), un altro termine per la stessa cosa. Nel mondo del database, l'API viene usata per descrivere SQL: SQL è l'API per un sistema DBMS.  
  
 Di queste scelte, Embedded SQL è l'uso più comune, anche se la maggior parte dei DBMS principali supporta interfacce della riga proprietari.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Elaborazione di un'istruzione SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL incorporato](../../odbc/reference/embedded-sql.md)  
  
-   [Moduli SQL](../../odbc/reference/sql-modules.md)  
  
-   [Call Level Interface](../../odbc/reference/call-level-interfaces.md)
