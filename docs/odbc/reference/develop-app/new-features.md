---
title: Nuove funzionalità | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4582a99797d5f6035f6d5d639514c5a6fdd572d
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794061"
---
# <a name="new-features"></a>Nuove funzionalità
In ODBC è stata introdotta la nuova funzionalità seguente *3.x*. Un database ODBC *3.x* funziona con un database ODBC *2.x* driver non sarà in grado di usare questa funzionalità. ODBC *3.x* gestione Driver non eseguire il mapping di queste funzionalità quando si lavora con un database ODBC *2.x* driver.  
  
-   Le funzioni che accettano un descrittore di handle come argomento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, and **SQLCopyDesc**.  
  
-   Le funzioni **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   L'uso di **SQLAllocHandle** per allocare un handle di descrittore. (L'uso di **SQLAllocHandle** per allocare gli handle di ambiente, connessione e istruzione è una funzionalità non nuova e duplicate.)  
  
-   L'uso di **SQLGetConnectAttr** per ottenere gli attributi di connessione SQL_ATTR_AUTO_IPD. (L'uso di **SQLSetConnectAttr** per impostare, e **SQLGetConnectAttr** per ottenere, altri attributi di connessione è una funzionalità non nuova e duplicate.)  
  
-   L'uso di **SQLSetStmtAttr** per impostare, e **SQLGetStmtAttr** per ottenere i seguenti attributi di istruzione. (L'uso di **SQLSetStmtAttr** per impostare, e **SQLGetStmtAttr** per ottenere, altri attributi di istruzione è una funzionalità non nuova e duplicate.)  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   L'uso di **SQLGetStmtAttr** per ottenere i seguenti attributi di istruzione. (L'uso di **SQLGetStmtAttr** per ottenere un'altra istruzione degli attributi è una funzionalità duplicate, non nuove funzionalità.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso del tipo di dati di intervallo C, i tipi di dati di intervallo SQL, i tipi di dati BIGINT C e la struttura di data SQL_C_NUMERIC.  
  
-   L'associazione di parametri.  
  
-   Offset in base al segnalibro recupera, ad esempio la chiamata **SQLFetchScroll** con un *FetchOrientation* argomento di SQL_FETCH_BOOKMARK e specificando un offset diverso da 0.  
  
-   **SQLFetch** che restituisce la matrice di stato di riga, numero di righe recuperate, il recupero di più righe, combinare le chiamate con **SQLFetchScroll**e combinare le chiamate con **SQLBulkOperations** o **SQLSetPos**. Per altre informazioni, vedere la sezione successiva [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parametri denominati.  
  
-   Uno qualsiasi dei ODBC *3.x*-specifici **SQLGetInfo** opzioni. (Se un database ODBC *3.x* funziona con un database ODBC *2.x* driver chiama i tipi di informazioni SQL_XXX_CURSOR_ATTRIBUTES1, che sono sostituiti ODBC diversi *2.x* tipi di informazioni, alcune informazioni potrebbero essere affidabile, ma alcuni potrebbero non essere affidabili. Per altre informazioni, vedere [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Associare gli offset.  
  
-   L'aggiornamento, aggiornamento ed eliminazione per i segnalibri (tramite una chiamata a **SQLBulkOperations**).  
  
-   La chiamata **SQLBulkOperations** oppure **SQLSetPos** nello stato S5.  
  
-   I campi ROW_NUMBER e col nel record di diagnostica (che devono essere recuperati dalle funzioni di sostituzione **SQLGetDiagField** oppure **SQLGetDiagRec**).  
  
-   Conteggio righe approssimative.  
  
-   Le informazioni sull'avviso (da SQL_ROW_SUCCESS_WITH_INFO **SQLFetchScroll**).  
  
-   Segnalibri di lunghezza variabile.  
  
-   Informazioni dettagliate sull'errore per le matrici di parametri.  
  
-   Tutte le nuove colonne in set di risultati restituiti dalle funzioni di catalogo.  
  
-   Sfrutta **SQLDescribeCol** e **SQLColAttribute** sulla colonna 0.  
  
-   Uso di qualsiasi ODBC *3.x*-attributi di colonna specifica in una chiamata a **SQLColAttribute**.  
  
-   Utilizzo di più handle di ambiente.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
