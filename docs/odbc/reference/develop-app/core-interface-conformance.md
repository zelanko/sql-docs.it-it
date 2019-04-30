---
title: Conformità di interfaccia di base | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e41d71cd3651e1db5d1a533159012b645b8c7764
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043760"
---
# <a name="core-interface-conformance"></a>Conformità di interfaccia Core
Tutti i driver ODBC devono includere almeno a livello di base della conformità di interfaccia. Poiché le funzionalità di livello principale sono quelle richieste dalle applicazioni interoperative più generiche, il driver può lavorare con tali applicazioni. Le funzionalità di livello principale corrispondono anche alle funzionalità definite nella specifica ISO CLI e con le funzionalità necessari definite nella specifica Open dell'interfaccia della riga di gruppo. Un driver ODBC di interfaccia conformi a livello di base consente all'applicazione di eseguire tutte le operazioni seguenti:  
  
-   Alloca e libera tutti i tipi di handle, chiamando **SQLAllocHandle** e **SQLFreeHandle**.  
  
-   Tutte le forme di usare la **SQLFreeStmt** (funzione).  
  
-   Associare colonne del set di risultati, chiamando **SQLBindCol**.  
  
-   Gestire i parametri dinamici, incluse le matrici di parametri, l'input solo in direzione, chiamando **SQLBindParameter** e **SQLNumParams**. (I parametri nella direzione output sono funzionalità 203 nelle [conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Specificare un offset di associazione.  
  
-   Utilizzare la finestra di dialogo data-at-execution, che includono chiamate a **SQLParamData** e **SQLPutData**.  
  
-   Gestire i cursori e nomi di cursore, chiamando **SQLCloseCursor**, **SQLGetCursorName**, e **SQLSetCursorName**.  
  
-   Ottenere l'accesso alla descrizione (metadati) del set di risultati, chiamando **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, e **SQLRowCount** . (Uso di queste funzioni sul numero di colonna 0 per recuperare i metadati del segnalibro è funzionalità 204 nelle [conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Eseguire una query il dizionario dei dati, chiamando le funzioni di catalogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, e **SQLTables**.  
  
     Il driver non è necessario per supportare i nomi composti da più parti di tabelle di database e le viste. (Per altre informazioni, vedere funzionalità 101 [conformità di interfaccia di livello 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) e di funzionalità 201 nel [conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) Tuttavia, alcune funzionalità della specifica SQL-92, ad esempio qualificazione di colonna e i nomi di indici, sono sintatticamente simili alla denominazione multipart. Il presenta elenco di funzioni ODBC non deve introdurre nuove opzioni in questi aspetti di SQL-92.  
  
-   Gestire origini dati e connessioni, chiamando **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, e **SQLDriverConnect**. Ottenere informazioni sul driver, indipendentemente da quale ODBC livello che supportano, chiamando **SQLDrivers**.  
  
-   Preparare ed eseguire istruzioni SQL, chiamando **SQLExecDirect**, **SQLExecute**, e **SQLPrepare**.  
  
-   Recuperare una riga di un set di risultati o più righe, in avanti, solo chiamando **SQLFetch** oppure chiamando **SQLFetchScroll** con il *FetchOrientation* argomento Impostare su SQL_FETCH_NEXT.  
  
-   Ottenere una colonna non associata in parti, chiamando **SQLGetData**.  
  
-   Ottenere i valori correnti di tutti gli attributi, chiamando **SQLGetConnectAttr**, **SQLGetEnvAttr**, e **SQLGetStmtAttr**e impostare gli attributi di tutti i valori predefiniti e impostare determinati attributi per valori non predefiniti chiamando **SQLSetConnectAttr**, **SQLSetEnvAttr**, e **SQLSetStmtAttr**.  
  
-   Modificare alcuni campi di descrittori, chiamando **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, e **SQLSetDescRec**.  
  
-   Ottenere le informazioni di diagnostica, chiamando **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   Rilevare le funzionalità del driver, chiamando **SQLGetFunctions** e **SQLGetInfo**. Inoltre, di rilevare il risultato di tutte le sostituzioni di testo apportate a un'istruzione SQL prima che venga inviata all'origine dati, chiamando **SQLNativeSql**.  
  
-   Usare la sintassi del **SQLEndTran** al commit di una transazione. Un driver di livello principale non deve necessariamente supportare le transazioni true. Pertanto, l'applicazione non è possibile specificare SQL_ROLLBACK né SQL_AUTOCOMMIT_OFF per l'attributo di connessione SQL_ATTR_AUTOCOMMIT. (Per altre informazioni, vedere funzionalità 109 [conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Chiamare **SQLCancel** per annullare la finestra di dialogo data-at-execution e, in ambienti multithread, per annullare un'esecuzione di funzione ODBC in un altro thread. Conformità di interfaccia di livello di base non implica il supporto per l'esecuzione asincrona delle funzioni, né l'uso di **SQLCancel** per annullare una funzione ODBC in esecuzione in modo asincrono. La piattaforma né il driver ODBC devono essere multithread per il driver eseguire le attività indipendenti nello stesso momento. Tuttavia, negli ambienti multithread, il driver ODBC deve essere thread-safe. Serializzazione delle richieste dall'applicazione è una soluzione alternativa per implementare questa specifica, anche se potrebbe creare seri problemi di prestazioni.  
  
-   Ottenere la colonna SQL_BEST_ROWID identificazione delle righe delle tabelle, chiamando **SQLSpecialColumns**. (Il supporto per SQL_ROWVER è funzionalità 208 nelle [conformità di interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Driver ODBC deve implementare le funzioni al livello di conformità di interfaccia Core.
