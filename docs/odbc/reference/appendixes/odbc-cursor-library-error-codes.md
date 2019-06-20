---
title: Codici di errore della libreria di cursore ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1fb077261eda4b2e013abd6d87e894637a29216a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181237"
---
# <a name="odbc-cursor-library-error-codes"></a>Codici di errore della libreria di cursori ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Microsoft Data Access Components. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Usare invece i cursori di driver e del server.  
  
 La libreria di cursori ODBC restituisce il SQLSTATEs seguenti oltre a quelli elencati [riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La libreria di cursori non sono ordinati; record di stato Gestione Driver e ODBC 3. *x* i driver sono responsabili per l'ordinamento dei record di stato.  
  
|SQLSTATE|Descrizione|Può essere restituito da|  
|--------------|-----------------|--------------------------|  
|01000|Cursore non è aggiornabile.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|Libreria di cursori non utilizzata. Caricamento non riuscito.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Libreria di cursori non utilizzata. Supporto dei driver insufficienti.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Libreria di cursori non utilizzata. Mancata corrispondenza delle versioni con gestione Driver.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Driver restituito SQL_SUCCESS_WITH_INFO. Il messaggio di avviso è stata perso.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Errore generale: Impossibile creare il buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: Impossibile leggere dal buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: Impossibile scrivere nel buffer di file.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Errore generale: Non è possibile chiudere o rimuovere i buffer di file.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Impossibile eseguire richieste posizionate perché nessuna colonna ricercabile associata.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|Richiesta posizionato potrebbe non essere eseguita perché set di risultati è stato creato da una condizione di join.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Il buffer associato supera la dimensione massima del segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Set di risultati non è stato generato da un **seleziona** istruzione.|**SQLGetData**|  
|SL005|**Selezionare** istruzione contiene una clausola GROUP BY.|**SQLGetData**|  
|SL006|Matrici di parametri non sono supportate con le richieste di posizionamento.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** non è consentita su un cursore forward-only (senza buffer).|**SQLGetData**|  
|SL009|Nessuna colonna associata prima di chiamare **SQLFetch** oppure **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** restituito SQL_ERROR durante un tentativo di associare a un buffer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|L'opzione dell'istruzione è valida solo dopo la chiamata **SQLFetch** oppure **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Associazioni di istruzione non possono essere modificate mentre è aperto un cursore.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|È stata emessa una richiesta di posizione e non tutti i campi numero di colonna sono stati memorizzati nel buffer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** e **SQLFetchScroll** non possono essere combinate.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
