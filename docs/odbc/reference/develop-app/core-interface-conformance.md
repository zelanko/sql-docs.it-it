---
title: Conformità dell'interfaccia di base Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302133"
---
# <a name="core-interface-conformance"></a>Conformità di interfaccia Core
Tutti i driver ODBC devono presentare almeno conformità all'interfaccia di livello Core.All ODBC drivers must exhibit at least Core-level interface conformance. Poiché le funzionalità di livello Core sono quelle richieste dalla maggior parte delle applicazioni interoperabili generiche, il driver può lavorare con tali applicazioni. Le funzionalità del livello Core corrispondono anche alle funzionalità definite nella specifica ISO CLI e alle funzionalità non facoltative definite nella specifica Open Group CLI. Un driver ODBC conforme all'interfaccia di livello Core consente all'applicazione di eseguire tutte le operazioni seguenti:A Core-level interface-conformant ODBC driver allows the application to do all of the following:  
  
-   Allocare e liberare tutti i tipi di handle, chiamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Utilizzare tutte le forme della funzione **SQLFreeStmt.**  
  
-   Associare le colonne del set di risultati chiamando **SQLBindCol**.  
  
-   Gestire i parametri dinamici, incluse le matrici di parametri, solo nella direzione di input, chiamando **SQLBindParameter** e **SQLNumParams**. (I parametri nella direzione di uscita sono feature 203 in [Conformità dell'interfaccia](../../../odbc/reference/develop-app/level-2-interface-conformance.md)di livello 2 .)  
  
-   Specificare un offset di associazione.  
  
-   Utilizzare la finestra di dialogo data-at-execution, che coinvolge le chiamate a **SQLParamData** e **SQLPutData**.  
  
-   Gestire i cursori e i nomi dei cursori, chiamando **SQLCloseCursor**, **SQLGetCursorName**e **SQLSetCursorName**.  
  
-   Ottenere l'accesso alla descrizione (metadati) dei set di risultati, chiamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**e **SQLRowCount**. L'uso di queste funzioni sul numero di colonna 0 per recuperare i metadati dei segnalibri è la funzionalità 204 nella [conformità dell'interfaccia](../../../odbc/reference/develop-app/level-2-interface-conformance.md)di livello 2.  
  
-   Eseguire una query sul dizionario dei dati chiamando le funzioni di catalogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**e **SQLTables**.  
  
     Il driver non è necessario per supportare i nomi in più parti di tabelle e viste di database. (Per ulteriori informazioni, vedere la funzionalità 101 in [Livello 1 Interfaccia Conformità](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e funzionalità 201 in Conformità interfaccia di livello [2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) Tuttavia, alcune funzionalità della specifica SQL-92, ad esempio la qualificazione delle colonne e i nomi degli indici, sono sintatticamente paragonabili alla denominazione multiparte. L'elenco presente delle funzionalità ODBC non è destinato a introdurre nuove opzioni in questi aspetti di SQL-92.  
  
-   Gestire le origini dati e le connessioni chiamando **SQLConnect**, **SQLDataSources**, **SQLDisconnect**e **SQLDriverConnect**. Ottenere informazioni sui driver, indipendentemente dal livello ODBC supportato, chiamando **SQLDrivers**.  
  
-   Preparare ed eseguire istruzioni SQL, chiamando **SQLExecDirect**, **SQLExecute**e **SQLPrepare**.  
  
-   Recuperare una riga di un set di risultati o più righe, solo nella direzione in avanti, chiamando **SQLFetchO** o chiamando **SQLFetchScroll** con il *FetchOrientation* argomento impostato su SQL_FETCH_NEXT.  
  
-   Ottenere una colonna non associata in parti, chiamando **SQLGetData**.  
  
-   Ottenere i valori correnti di tutti gli attributi, chiamando **SQLGetConnectAttr**, **SQLGetEnvAttr**e **SQLGetStmtAttr**e impostare tutti gli attributi sui valori predefiniti e impostare determinati attributi su valori non predefiniti chiamando **SQLSetConnectAttr**, **SQLSetEnvAttr**e **SQLSetStmtAttr**.  
  
-   Modificare determinati campi dei descrittori chiamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**e **SQLSetDescRec**.  
  
-   Ottenere informazioni di diagnostica chiamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Rilevare le funzionalità dei driver chiamando **SQLGetFunctions** e **SQLGetInfo**. Inoltre, rilevare il risultato di eventuali sostituzioni di testo apportate a un'istruzione SQL prima che venga inviata all'origine dati, chiamando **SQLNativeSql**.  
  
-   Utilizzare la sintassi di **SQLEndTran** per eseguire il commit di una transazione. Un driver di livello Core non deve supportare le transazioni true; pertanto, l'applicazione non può specificare SQL_ROLLBACK né SQL_AUTOCOMMIT_OFF per l'attributo di connessione SQL_ATTR_AUTOCOMMIT. (Per ulteriori informazioni, vedere la funzionalità 109 in [Conformità interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Chiamare **SQLCancel** per annullare la finestra di dialogo data-at-execution e, in ambienti multithread, per annullare una funzione ODBC in esecuzione in un altro thread. La conformità dell'interfaccia di livello base non impone il supporto per l'esecuzione asincrona delle funzioni, né l'utilizzo di **SQLCancel** per annullare l'esecuzione asincrona di una funzione ODBC. Né la piattaforma né il driver ODBC devono essere multithread per il driver per condurre attività indipendenti allo stesso tempo. Tuttavia, negli ambienti multithread, il driver ODBC deve essere thread-safe. La serializzazione delle richieste dall'applicazione è un modo conforme per implementare questa specifica, anche se potrebbe creare gravi problemi di prestazioni.  
  
-   Ottenere la SQL_BEST_ROWID colonna di tabelle di identificazione di riga, chiamando **SQLSpecialColumns**. (Supporto per SQL_ROWVER è la funzionalità 208 in [Conformità interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  I driver ODBC devono implementare le funzioni nel livello di conformità dell'interfaccia Core.ODBC Drivers must implement the functions in the Core interface conformance level.
