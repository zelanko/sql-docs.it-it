---
title: Prendere in considerazione le funzionalità di Database da utilizzare | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92eeb64b95d666b15c03c70d656d2309a63eabf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042187"
---
# <a name="considering-database-features-to-use"></a>Considerazione delle funzionalità di database da usare
Una volta noto il livello di base dell'interoperabilità, è necessario considerare le funzionalità di database usate dall'applicazione. Ad esempio, quali istruzioni SQL hanno l'applicazione eseguirà? L'applicazione userà i cursori scorrevoli? Transazioni? Procedure? Dati di tipo Long? Per idee sulle funzionalità potrebbero non essere supportate da tutti i DBMS, vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) le descrizioni delle funzioni e [ Appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Le funzionalità richieste da un'applicazione potrebbero eliminare alcuni DBMS dall'elenco di DBMS di destinazione. Si potrebbe anche essere indicato che l'applicazione può fare facilmente riferimento maggior parte dei DBMS.  
  
 Ad esempio, se le funzionalità necessarie sono semplici, ma essere implementati in genere con un elevato livello di interoperabilità. Un'applicazione che esegue una semplice **seleziona** istruzione e recupera i risultati con cursori forward-only è probabile che sia altamente interoperabile, grazie alla relativa semplicità: Quasi tutti i driver e DBMS supportano le funzionalità che necessarie.  
  
 Tuttavia, se le funzionalità necessarie sono più complesse, ad esempio cursori scorrevoli, per gli aggiornamenti posizionati e istruzioni delete e procedure, i compromessi spesso dovuti. Esistono diverse possibilità:  
  
-   **Interoperabilità inferiore, più funzionalità.** L'applicazione include le funzionalità ma funziona solo con DBMS che li supportano.  
  
-   **Maggiore interoperabilità, meno funzionalità.** L'applicazione elimina le funzionalità ma funziona con altre DBMS.  
  
-   **Maggiore interoperabilità, funzionalità facoltative.** L'applicazione include le funzionalità, ma li rende disponibili solo con tali DBMS che li supportano.  
  
-   **Maggiore interoperabilità, altre funzionalità.** L'applicazione utilizza le caratteristiche con DBMS che li supportano ed emula li per DBMS che non li supportano.  
  
 I primi due casi sono relativamente semplici da implementare, poiché le funzionalità vengono utilizzate con tutti i DBMS supportati o con nessuno. Ultimi due casi, d'altra parte, sono più complessi. È necessario in entrambi i casi per verificare se il sistema DBMS supporta le funzionalità e nell'ultimo caso per scrivere una grande quantità di codice per emulare queste funzionalità. Pertanto, questi schemi sono probabilmente saranno necessarie altre fase di sviluppo e potrebbero essere più lenti in fase di esecuzione.  
  
 Si consideri un'applicazione di query standard che può connettersi a una singola origine dati. L'applicazione accetta una query da parte dell'utente e visualizza i risultati in una finestra. Ora si supponga che l'applicazione è una funzionalità che consente agli utenti di visualizzare i risultati di più query contemporaneamente. Ovvero sono può eseguire una query e di esaminare alcune dei risultati eseguire una query diversa ed esaminare alcuni dei relativi risultati e quindi tornare alla query prima. Questo presenta un problema di interoperabilità, perché alcuni driver supportano solo una singola istruzione attiva.  
  
 L'applicazione ha un numero di scelte, basate su ciò che il driver restituisce per l'opzione di SQL_MAX_CONCURRENT_ACTIVITIES **SQLGetInfo**:  
  
-   **Supporta sempre più query.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. Se il driver supporta solo un'istruzione attiva, l'applicazione viene chiusa la connessione e avvisa l'utente che il driver non supporta la funzionalità richiesta. L'applicazione è facile da implementare e ha funzionalità complete ma interoperabilità inferiore.  
  
-   **Non supporta più query.** L'applicazione elimina completamente la funzionalità. È facile da implementare e ha l'interoperabilità elevata ma dispone di meno funzionalità.  
  
-   **Supporta più query solo se il driver non.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione consente all'utente di avviare una nuova istruzione quando è già attivo solo se il driver supporta più istruzioni attive. L'applicazione dispone di maggiore funzionalità e l'interoperabilità, ma è molto difficile implementare.  
  
-   **Sempre supportano più query ed emularli quando necessario.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione sempre consente all'utente di avviare una nuova istruzione quando è già attivo. Se il driver supporta solo un'istruzione attiva, l'applicazione apre una connessione aggiuntiva alle tale driver ed esegue l'istruzione nuova in tale connessione. L'applicazione dispone di tutte le funzionalità e interoperabilità elevata ma è molto difficile implementare.
