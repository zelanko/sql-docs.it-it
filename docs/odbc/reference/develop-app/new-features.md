---
description: Nuove funzioni e caratteristiche
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2015d424e0c755352fa66f3ac67503b612b6982f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429233"
---
# <a name="new-features"></a>Nuove funzioni e caratteristiche
Le seguenti nuove funzionalità sono state introdotte in ODBC *3. x*. Un'applicazione ODBC *3. x* che utilizza un driver ODBC *2. x* non sarà in grado di utilizzare questa funzionalità. Gestione driver ODBC *3. x* non esegue il mapping di queste funzionalità quando si utilizza un driver ODBC *2. x* .  
  
-   Funzioni che accettano un handle di descrittore come argomento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**e **SQLCopyDesc**.  
  
-   Funzioni **SQLSetEnvAttr** e **SQLGetEnvAttr**.  
  
-   Utilizzo di **SQLAllocHandle** per allocare un handle del descrittore. (L'utilizzo di **SQLAllocHandle** per allocare gli handle di ambiente, di connessione e di istruzione è duplicato, non nuovo, funzionalità).  
  
-   Utilizzo di **SQLGetConnectAttr** per ottenere gli attributi di connessione SQL_ATTR_AUTO_IPD. (L'uso di **SQLSetConnectAttr** per impostare e **SQLGetConnectAttr** per ottenere, altri attributi di connessione sono duplicati, non nuovi, funzionalità).  
  
-   L'uso di **SQLSetStmtAttr** per impostare e **SQLGetStmtAttr** per ottenere gli attributi dell'istruzione seguenti. (L'uso di **SQLSetStmtAttr** per impostare e **SQLGetStmtAttr** da ottenere, altri attributi di istruzione sono duplicati, non nuovi, funzionalità).  
  
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
  
-   Utilizzo di **SQLGetStmtAttr** per ottenere gli attributi dell'istruzione seguenti. (L'uso di **SQLGetStmtAttr** per ottenere altri attributi di istruzione è una funzionalità duplicata, non una nuova funzionalità).  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Viene utilizzato il tipo di dati interval C, i tipi di dati interval SQL, i tipi di dati BIGINT C e la struttura dei dati SQL_C_NUMERIC.  
  
-   Associazione di parametri per riga.  
  
-   Recupero di segnalibri basati su offset, ad esempio la chiamata a **SQLFetchScroll** con un argomento *FetchOrientation* di SQL_FETCH_BOOKMARK e la specifica di un offset diverso da 0.  
  
-   **SQLFetch** che restituisce la matrice di stato della riga, il numero di righe recuperate, il recupero di più righe, la combinazione di chiamate con **SQLFetchScroll**e la combinazione di chiamate con **SQLBulkOperations** o **SQLSetPos**. Per ulteriori informazioni, vedere la sezione successiva, [bloccare i cursori, i cursori scorrevoli e la compatibilità con le versioni precedenti per le applicazioni ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parametri denominati.  
  
-   Tutte le opzioni **SQLGetInfo** specifiche di ODBC *3. x*. Se un'applicazione ODBC *3. x* che utilizza un driver ODBC *2. x* chiama i tipi di informazioni SQL_XXX_CURSOR_ATTRIBUTES1, che hanno sostituito diversi tipi di informazioni ODBC *2. x* , alcune informazioni potrebbero essere affidabili, ma alcune potrebbero non essere affidabili. Per ulteriori informazioni, vedere [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
-   Offset di binding.  
  
-   Aggiornamento, aggiornamento ed eliminazione da segnalibri (tramite una chiamata a **SQLBulkOperations**).  
  
-   Chiamata di **SQLBulkOperations** o **SQLSetPos** nello stato S5.  
  
-   I campi ROW_NUMBER e COLUMN_NUMBER nel record di diagnostica (che devono essere recuperati dalle funzioni di sostituzione **SQLGetDiagField** o **SQLGetDiagRec**).  
  
-   Conteggio approssimativo delle righe.  
  
-   Informazioni sugli avvisi (SQL_ROW_SUCCESS_WITH_INFO da **SQLFetchScroll**).  
  
-   Segnalibri a lunghezza variabile.  
  
-   Informazioni estese sull'errore per le matrici di parametri.  
  
-   Tutte le nuove colonne nei set di risultati restituiti dalle funzioni di catalogo.  
  
-   Utilizzo di **SQLDescribeCol** e **SQLColAttribute** sulla colonna 0.  
  
-   Utilizzo di qualsiasi attributo di colonna specifico di ODBC *3. x*in una chiamata a **SQLColAttribute**.  
  
-   Utilizzo di più handle di ambiente.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti per le applicazioni ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
