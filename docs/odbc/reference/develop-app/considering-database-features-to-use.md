---
description: Considerazione delle funzionalità di database da usare
title: Considerazioni sulle funzionalità di database da utilizzare | Microsoft Docs
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
ms.openlocfilehash: 2abaed3806514a161c5c506d8bad89b4d3b75153
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465893"
---
# <a name="considering-database-features-to-use"></a>Considerazione delle funzionalità di database da usare
Una volta definito il livello di interoperabilità di base, è necessario prendere in considerazione le funzionalità di database utilizzate dall'applicazione. Ad esempio, quali istruzioni SQL eseguiranno l'applicazione? L'applicazione utilizzerà cursori scorrevoli? Transazioni? Procedure? Dati lunghi? Per le idee sulle funzionalità che potrebbero non essere supportate da tutti i sistemi DBMS, vedere le descrizioni delle funzioni [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)e [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) e l' [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md). Le funzionalità richieste da un'applicazione potrebbero eliminare alcuni DBMS dall'elenco dei DBMS di destinazione. Potrebbero inoltre indicare che l'applicazione può essere destinata facilmente a molti DBMS.  
  
 Se, ad esempio, le funzionalità richieste sono semplici, in genere possono essere implementate con un elevato livello di interoperabilità. Un'applicazione che esegue una semplice istruzione **Select** e recupera i risultati con un cursore di sola trasmissione è probabilmente altamente interoperativa grazie alla sua semplicità: quasi tutti i driver e i DBMS supportano la funzionalità necessaria.  
  
 Tuttavia, se le funzionalità richieste sono più complesse, ad esempio i cursori scorrevoli, le istruzioni di aggiornamento e eliminazione posizionate, nonché le procedure, è necessario che vengano spesso compromessi. Sono disponibili diverse possibilità:  
  
-   **Interoperabilità inferiore, altre funzionalità.** L'applicazione include le funzionalità, ma funziona solo con i sistemi DBMS che li supportano.  
  
-   **Interoperabilità più elevata, meno funzionalità.** L'applicazione rilascia le funzionalità ma funziona con più DBMS.  
  
-   **Maggiore interoperabilità, funzionalità facoltative.** L'applicazione include le funzionalità ma le rende disponibili solo con i DBMS che li supportano.  
  
-   **Maggiore interoperabilità, altre funzionalità.** L'applicazione usa le funzionalità con DBMS che le supportano e le emula per i sistemi DBMS che non lo supportano.  
  
 I primi due casi sono relativamente semplici da implementare, perché le funzionalità vengono usate con tutti i DBMS supportati o con nessuno. Gli ultimi due casi, d'altra parte, sono più complessi. In entrambi i casi è necessario controllare se il sistema DBMS supporta le funzionalità e nell'ultimo caso scrivere una quantità potenzialmente elevata di codice per emulare queste funzionalità. Pertanto, è probabile che questi schemi richiedano più tempo di sviluppo e potrebbero risultare più lenti in fase di esecuzione.  
  
 Si consideri un'applicazione di query generica in grado di connettersi a una singola origine dati. L'applicazione accetta una query dall'utente e Visualizza i risultati in una finestra. Si supponga ora che questa applicazione disponga di una funzionalità che consente agli utenti di visualizzare contemporaneamente i risultati di più query. Ovvero, possono eseguire una query ed esaminare alcuni dei risultati, eseguire una query diversa ed esaminare alcuni dei risultati, quindi tornare alla prima query. Si tratta di un problema di interoperabilità perché alcuni driver supportano solo una singola istruzione attiva.  
  
 L'applicazione ha diverse opzioni, in base a ciò che il driver restituisce per l'opzione SQL_MAX_CONCURRENT_ACTIVITIES in **SQLGetInfo**:  
  
-   **Supporta sempre più query.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. Se il driver supporta una sola istruzione attiva, l'applicazione chiude la connessione e informa l'utente che il driver non supporta la funzionalità richiesta. L'applicazione è facile da implementare e presenta funzionalità complete ma ha un'interoperabilità ridotta.  
  
-   **Non supportare mai più query.** L'applicazione rilascia completamente la funzionalità. È facile da implementare e offre un'interoperabilità elevata, ma ha meno funzionalità.  
  
-   **Supportare più query solo se il driver lo esegue.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione consente all'utente di avviare una nuova istruzione quando una è già attiva solo se il driver supporta più istruzioni attive. L'applicazione ha funzionalità e interoperabilità più elevate, ma è più difficile da implementare.  
  
-   **Supporta sempre più query e le emula quando necessario.** Dopo la connessione a un driver, l'applicazione controlla il numero di istruzioni attive. L'applicazione consente sempre all'utente di avviare una nuova istruzione quando una è già attiva. Se il driver supporta una sola istruzione attiva, l'applicazione apre una connessione aggiuntiva a tale driver ed esegue la nuova istruzione su tale connessione. L'applicazione ha funzionalità complete e interoperabilità elevata, ma è più difficile da implementare.
