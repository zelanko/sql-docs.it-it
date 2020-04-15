---
title: Codici di errore della libreria del cursore ODBC - Documenti Microsoft
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
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301432"
---
# <a name="odbc-cursor-library-error-codes"></a>Codici di errore della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Microsoft Data Access Component. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Utilizzare invece i cursori del driver e del server.  
  
 La libreria di cursori ODBC restituisce i seguenti SQLSTATEs oltre a quelli elencati in [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La libreria di cursori non ordina i record di stato; Gestione Driver e ODBC 3. *x* i driver sono responsabili dell'ordinazione dei record di stato.  
  
|SQLSTATE|Descrizione|Può essere restituito da|  
|--------------|-----------------|--------------------------|  
|01000|Il cursore non è aggiornabile.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Libreria di cursori non utilizzata. Caricamento non riuscito.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Libreria di cursori non utilizzata. Supporto del driver insufficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Libreria di cursori non utilizzata. Versione non corrispondente a Gestione Driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Il conducente ha restituito SQL_SUCCESS_WITH_INFO. Il messaggio di avviso è stato perso.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000 (in questo s2)|Errore generale: impossibile creare il buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000 (in questo s2)|Errore generale: impossibile leggere dal buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000 (in questo s2)|Errore generale: impossibile scrivere nel buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000 (in questo s2)|Errore generale: impossibile chiudere o rimuovere il buffer di file.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Impossibile eseguire la richiesta posizionata perché non sono state associate colonne ricercabili.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002 (in questo s2)|Impossibile eseguire la richiesta posizionata perché il set di risultati è stato creato da una condizione di join.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Il buffer associato supera la dimensione massima del segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Il set di risultati non è stato generato da un'istruzione **SELECT.**|**SQLGetData**|  
|SL005|**L'istruzione SELECT** contiene una clausola GROUP BY.|**SQLGetData**|  
|SL006|Le matrici di parametri non sono supportate con le richieste posizionate.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** non è consentito in un cursore forward-only (senza buffer).|**SQLGetData**|  
|SL009|Nessuna colonna è stata associata prima di chiamare **SQLFetch** o **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010 (informazioni in due)|**SQLBindCol** ha restituito SQL_ERROR durante un tentativo di associazione a un buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011 (informazioni in base alla|L'opzione di istruzione è valida solo dopo aver chiamato **SQLFetch** o **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012 (in questo sweboghino).|Le associazioni di istruzioni non possono essere modificate mentre è aperto un cursore.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014 (informazioni in base alla|È stata emessa una richiesta posizionata e non tutti i campi di conteggio delle colonne sono stati memorizzati nel buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015 (in modo sl)|**SQLFetch** e **SQLFetchScroll** non possono essere combinati.|**Sqlextendedfetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
