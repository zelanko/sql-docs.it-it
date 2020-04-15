---
title: Nuove funzionalità - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302399"
---
# <a name="new-features"></a>Nuove funzionalità
La seguente nuova funzionalità è stata introdotta in ODBC *3.x*. Un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* non sarà in grado di utilizzare questa funzionalità. Gestione Driver ODBC *3.x* non esegue il mapping di queste funzionalità quando si lavora con un driver ODBC *2.x.*  
  
-   Le funzioni che accettano un handle descrittore come argomento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**e **SQLCopyDesc**.  
  
-   Le funzioni **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   Utilizzo di **SQLAllocHandle** per allocare un handle di descrittore. L'utilizzo di **SQLAllocHandle** per allocare gli handle di ambiente, connessione e istruzione è duplicato, non nuovo, funzionalità.  
  
-   Utilizzo di **SQLGetConnectAttr** per ottenere gli attributi di connessione SQL_ATTR_AUTO_IPD. (L'utilizzo di **SQLSetConnectAttr** per impostare, e **SQLGetConnectAttr** per ottenere, altri attributi di connessione è duplicato, non nuovo, funzionalità.)  
  
-   Utilizzo di **SQLSetStmtAttr** per impostare e **SQLGetStmtAttr** per ottenere, gli attributi dell'istruzione seguenti. (L'utilizzo di **SQLSetStmtAttr** per impostare, e **SQLGetStmtAttr** per ottenere, altri attributi di istruzione è duplicato, non nuovo, funzionalità.)  
  
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
  
-   Utilizzo di **SQLGetStmtAttr** per ottenere gli attributi dell'istruzione seguenti. L'utilizzo di **SQLGetStmtAttr** per ottenere altri attributi dell'istruzione è una funzionalità duplicata, non una nuova funzionalità.  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Utilizzo del tipo di dati intervallo C, dei tipi di dati SQL a intervalli, dei tipi di dati BIGINT C e della struttura di dati SQL_C_NUMERIC.  
  
-   Associazione per riga dei parametri.  
  
-   Recupero di segnalibri basati su offset, ad esempio la chiamata **di SQLFetchScroll** con un FetchOrientation argomento di SQL_FETCH_BOOKMARK e la specifica di un offset diverso da 0.Offset-based bookmark fetches, such as calling SQLFetchScroll with a *FetchOrientation* argument of SQL_FETCH_BOOKMARK and specifying an offset other than 0.  
  
-   **SQLFetch** restituisce la matrice di stato della riga, il numero di righe recuperate, il recupero di più righe, l'intermixing delle chiamate con **SQLFetchScroll**e l'intermixing delle chiamate con **SQLBulkOperations** o **SQLSetPos**. Per ulteriori informazioni, vedere la sezione [successiva, Blocchi cursori, cursori scorrevoli e compatibilità con](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)le versioni precedenti per le applicazioni ODBC 3.x .  
  
-   Parametri denominati.  
  
-   Qualsiasi delle opzioni **SQLGetInfo** specifiche di ODBC *3.x.* (Se un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* chiama i tipi di informazioni SQL_XXX_CURSOR_ATTRIBUTES1, che hanno sostituito diversi tipi di informazioni ODBC *2.x,* alcune delle informazioni potrebbero essere affidabili, ma alcune potrebbero essere inaffidabili. Per altre informazioni, vedere [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Associare gli offset.  
  
-   Aggiornamento, aggiornamento ed eliminazione tramite segnalibri (tramite una chiamata a **SQLBulkOperations**).  
  
-   Chiamata di **SQLBulkOperations** o **SQLSetPos** nello stato S5.  
  
-   I campi ROW_NUMBER e COLUMN_NUMBER nel record di diagnostica, che devono essere recuperati dalle funzioni di sostituzione **SQLGetDiagField** o **SQLGetDiagRec**.  
  
-   Conteggio approssimativo delle righe.  
  
-   Informazioni di avviso (SQL_ROW_SUCCESS_WITH_INFO da **SQLFetchScroll**).  
  
-   Segnalibri a lunghezza variabile.  
  
-   Informazioni esprimono sugli errori per matrici di parametri.  
  
-   Tutte le nuove colonne nei set di risultati restituiti dalle funzioni di catalogo.  
  
-   Utilizzo di **SQLDescribeCol** e **SQLColAttribute** nella colonna 0.  
  
-   Utilizzo di qualsiasi attributo di colonna specifico di ODBC *3.x*in una chiamata a **SQLColAttribute**.  
  
-   Utilizzo di più handle di ambiente.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
