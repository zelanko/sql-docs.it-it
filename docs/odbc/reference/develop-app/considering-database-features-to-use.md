---
title: Considerare l'utilizzo delle funzionalità del database Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9d966781def1c3eab6a9568eab07ab591326171
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299011"
---
# <a name="considering-database-features-to-use"></a>Considerazione delle funzionalità di database da usare
Dopo aver conosciuto il livello di base di interoperabilità, è necessario considerare le funzionalità del database utilizzate dall'applicazione. Ad esempio, quali istruzioni SQL verranno eseguite dall'applicazione? L'applicazione utilizzerà cursori scorrevoli? Transazioni? Procedure? Dati lunghi? Per informazioni sulle funzionalità che potrebbero non essere supportate da tutti i DBSMO, vedere le descrizioni delle funzioni [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) e [Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Le funzionalità richieste da un'applicazione potrebbero eliminare alcuni DBSMO dall'elenco dei DBSMO di destinazione. Potrebbero anche dimostrare che l'applicazione può facilmente indirizzare molti DBS.  
  
 Ad esempio, se le funzionalità richieste sono semplici, in genere possono essere implementate con un elevato livello di interoperabilità. Un'applicazione che esegue una semplice istruzione **SELECT** e recupera i risultati con un cursore forward-only è probabile che sia altamente interoperabile in virtù della sua semplicità: quasi tutti i driver e DBMs supportano le funzionalità necessarie.  
  
 Tuttavia, se le funzionalità necessarie sono più complesse, ad esempio cursori scorrevoli, istruzioni di aggiornamento ed eliminazione posizionate e procedure, è spesso necessario effettuare compromessi. Ci sono diverse possibilità:  
  
-   **Minore interoperabilità, più funzionalità.** L'applicazione include le funzionalità, ma funziona solo con DBM che le supportano.  
  
-   **Maggiore interoperabilità, meno funzionalità.** L'applicazione elimina le funzionalità ma funziona con più DBS.  
  
-   **Maggiore interoperabilità, funzionalità facoltative.** L'applicazione include le funzionalità, ma le rende disponibili solo con i DBS che le supportano.  
  
-   **Maggiore interoperabilità, più funzionalità.** L'applicazione utilizza le funzionalità con DBSMO che li supportano e li emula per DBS che non lo supportano.  
  
 I primi due casi sono relativamente semplici da implementare, perché le funzionalità vengono utilizzate con tutti i DBS supportati o con nessuno. Questi ultimi due casi, d'altra parte, sono più complessi. In entrambi i casi è necessario verificare se il DBMS supporta le funzionalità e nell'ultimo caso scrivere una quantità potenzialmente grande di codice per emulare queste funzionalità. Pertanto, è probabile che questi schemi richiedano più tempo di sviluppo e potrebbero essere più lenti in fase di esecuzione.  
  
 Si consideri un'applicazione di query generica in grado di connettersi a una singola origine dati. L'applicazione accetta una query dall'utente e visualizza i risultati in una finestra. Si supponga ora che questa applicazione abbia una funzionalità che consente agli utenti di visualizzare i risultati di più query contemporaneamente. Ovvero, possono eseguire una query e esaminare alcuni dei risultati, eseguire una query diversa e esaminarne alcuni risultati e quindi tornare alla prima query. Ciò presenta un problema di interoperabilità perché alcuni driver supportano solo una singola istruzione attiva.  
  
 L'applicazione dispone di una serie di scelte, in base a ciò che il driver restituisce per l'opzione SQL_MAX_CONCURRENT_ACTIVITIES in **SQLGetInfo**:  
  
-   **Supporta sempre più query.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. Se il driver supporta una sola istruzione attiva, l'applicazione chiude la connessione e informa l'utente che il driver non supporta la funzionalità richiesta. L'applicazione è facile da implementare e ha funzionalità complete, ma ha una minore interoperabilità.  
  
-   **Non supporta mai più query.** L'applicazione elimina completamente la funzionalità. È facile da implementare e ha un'elevata interoperabilità, ma ha meno funzionalità.  
  
-   **Supporta più query solo se il driver lo fa.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione consente all'utente di avviare una nuova istruzione quando è già attivo solo se il driver supporta più istruzioni attive. L'applicazione ha funzionalità e interoperabilità più elevate, ma è più difficile da implementare.  
  
-   **Supporta sempre più query ed emulale quando necessario.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione consente sempre all'utente di avviare una nuova istruzione quando è già attiva. Se il driver supporta una sola istruzione attiva, l'applicazione apre una connessione aggiuntiva a tale driver ed esegue la nuova istruzione su tale connessione. L'applicazione ha funzionalità complete e un'elevata interoperabilità, ma è più difficile da implementare.
