---
description: Codici di errore della libreria di cursori ODBC
title: Codici di errore della libreria di cursori ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 414de02eb7145006af4faa543735888082a3d6ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466136"
---
# <a name="odbc-cursor-library-error-codes"></a>Codici di errore della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Microsoft Data Access Component. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Utilizzare invece i cursori driver e server.  
  
 La libreria di cursori ODBC restituisce i seguenti SQLSTATE, oltre a quelli elencati in [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La libreria di cursori non Ordina i record di stato; Gestione driver e ODBC 3. i driver *x* sono responsabili dell'ordinamento dei record di stato.  
  
|SQLSTATE|Descrizione|Può essere restituito da|  
|--------------|-----------------|--------------------------|  
|01000|Cursore non aggiornabile.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Impossibile utilizzare la libreria di cursori. Il caricamento non è riuscito.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Impossibile utilizzare la libreria di cursori. Supporto driver insufficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Impossibile utilizzare la libreria di cursori. Versione non corrispondente a gestione driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Il driver ha restituito SQL_SUCCESS_WITH_INFO. Il messaggio di avviso è andato perso.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Errore generale: Impossibile creare il buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: Impossibile leggere dal buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: Impossibile scrivere nel buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: non è possibile chiudere o rimuovere il buffer di file.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Impossibile eseguire la richiesta posizionata perché non è stata associata alcuna colonna ricercabile.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|Impossibile eseguire la richiesta posizionata perché il set di risultati è stato creato da una condizione di join.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Il buffer associato supera la dimensione massima del segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Il set di risultati non è stato generato da un'istruzione **Select** .|**SQLGetData**|  
|SL005|L'istruzione **Select** contiene una clausola Group by.|**SQLGetData**|  
|SL006|Le matrici di parametri non sono supportate con le richieste posizionate.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** non è consentito in un cursore di sola trasmissione (non memorizzato nel buffer).|**SQLGetData**|  
|SL009|Nessuna colonna è stata associata prima della chiamata a **SQLFetch** o **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** ha restituito SQL_ERROR durante un tentativo di associazione a un buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|L'opzione Statement è valida solo dopo la chiamata a **SQLFetch** o **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Non è possibile modificare le associazioni di istruzioni mentre un cursore è aperto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|È stata eseguita una richiesta posizionata e non tutti i campi di conteggio delle colonne sono stati memorizzati nel buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** non possono essere combinati.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
