---
title: Conformità dell'interfaccia Core | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02e8aabf808ebf11f2e241fc7d330f794dbb0112
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002113"
---
# <a name="core-interface-conformance"></a>Conformità di interfaccia Core
Tutti i driver ODBC devono presentare almeno la conformità dell'interfaccia di base. Poiché le funzionalità del livello di base sono quelle richieste dalla maggior parte delle applicazioni interoperative generiche, il driver può funzionare con tali applicazioni. Le funzionalità del livello di base corrispondono anche alle funzionalità definite nella specifica dell'interfaccia della riga di comando ISO e alle funzionalità non facoltative definite nella specifica CLI del gruppo aperto. Un driver ODBC conforme all'interfaccia di livello principale consente all'applicazione di eseguire le operazioni seguenti:  
  
-   Allocare e liberare tutti i tipi di handle chiamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Usare tutti i form della funzione **SQLFreeStmt** .  
  
-   Associare le colonne del set di risultati chiamando **SQLBindCol**.  
  
-   Gestire i parametri dinamici, incluse le matrici di parametri, solo nella direzione di input, chiamando **SQLBindParameter** e **SQLNumParams**. (I parametri nella direzione dell'output sono la funzionalità 203 nella [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Specificare un offset di binding.  
  
-   Utilizzare la finestra di dialogo Data-at-execution, che include le chiamate a **SQLParamData** e **SQLPutData**.  
  
-   Gestire i cursori e i nomi dei cursori chiamando **SQLCloseCursor**, **SQLGetCursorName**e **SQLSetCursorName**.  
  
-   Ottenere l'accesso alla descrizione (metadati) dei set di risultati, chiamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**e **SQLRowCount**. (L'uso di queste funzioni nella colonna numero 0 per recuperare i metadati dei segnalibri è la funzionalità 204 nella [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Eseguire una query sul dizionario dei dati chiamando le funzioni di catalogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**e **SQLTables**.  
  
     Il driver non è necessario per supportare nomi multipart di tabelle e viste di database. Per altre informazioni, vedere funzionalità 101 in [conformità dell'interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e funzionalità 201 in [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md). Tuttavia, alcune funzionalità della specifica SQL-92, ad esempio la qualificazione di colonna e i nomi degli indici, sono sintatticamente confrontabili con la denominazione multipart. Il presente elenco di funzionalità ODBC non ha lo scopo di introdurre nuove opzioni in questi aspetti di SQL-92.  
  
-   Gestire le origini dati e le connessioni, chiamando **SQLConnect**, **SQLDataSources**, Disconnect e **SQLDriverConnect**. **** Ottenere informazioni sui driver, indipendentemente dal livello ODBC supportato, chiamando **SQLDrivers**.  
  
-   Preparare ed eseguire istruzioni SQL, chiamando **SQLExecDirect**, **SQLExecute**e **SQLPrepare**.  
  
-   Recuperare una riga di un set di risultati o più righe, solo nella direzione in avanti, chiamando **SQLFetch** o chiamando **SQLFetchScroll** con l'argomento *FetchOrientation* impostato su SQL_FETCH_NEXT.  
  
-   Ottenere una colonna non associata in parti, chiamando **SQLGetData**.  
  
-   Ottenere i valori correnti di tutti gli attributi chiamando **SQLGetConnectAttr**, **SQLGetEnvAttr**e **SQLGetStmtAttr**e impostare tutti gli attributi sui valori predefiniti e impostare determinati attributi su valori non predefiniti chiamando **SQLSetConnectAttr**, **SQLSetEnvAttr**e **SQLSetStmtAttr**.  
  
-   Modificare determinati campi dei descrittori, chiamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**e **SQLSetDescRec**.  
  
-   Ottenere informazioni di diagnostica, chiamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Rilevare le funzionalità del driver chiamando **SQLGetFunctions** e **SQLGetInfo**. Inoltre, è possibile rilevare il risultato di tutte le sostituzioni di testo apportate a un'istruzione SQL prima dell'invio all'origine dati, chiamando **SQLNativeSql**.  
  
-   Usare la sintassi di **SQLEndTran** per eseguire il commit di una transazione. Un driver di livello principale non deve supportare le transazioni true. Pertanto, l'applicazione non può specificare SQL_ROLLBACK né SQL_AUTOCOMMIT_OFF per l'attributo di connessione SQL_ATTR_AUTOCOMMIT. (Per altre informazioni, vedere funzionalità 109 nella [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Chiamare **SQLCancel** per annullare la finestra di dialogo Data-at-execution e, in ambienti multithread, per annullare una funzione ODBC in esecuzione in un altro thread. La conformità dell'interfaccia di livello principale non impone il supporto per l'esecuzione asincrona di funzioni, né l'utilizzo di **SQLCancel** per annullare una funzione ODBC in esecuzione in modo asincrono. Né la piattaforma né il driver ODBC devono essere multithread per il driver in modo da condurre attività indipendenti nello stesso momento. Tuttavia, negli ambienti multithread, il driver ODBC deve essere thread-safe. La serializzazione delle richieste dall'applicazione è un modo conforme per implementare questa specifica, anche se potrebbe creare gravi problemi di prestazioni.  
  
-   Ottenere la colonna di identificazione SQL_BEST_ROWID riga delle tabelle chiamando **SQLSpecialColumns**. Il supporto per SQL_ROWVER è la funzionalità 208 della [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).  
  
    > [!IMPORTANT]  
    >  I driver ODBC devono implementare le funzioni nel livello di conformità dell'interfaccia di base.
