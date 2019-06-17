---
title: Gestione driver&#39;s ruolo nel processo di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af81fd6c4b0b56474497a829985a754ccf88f3ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238022"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Gestione driver&#39;s ruolo nel processo di connessione
Tenere presente che le applicazioni non chiamano direttamente le funzioni di driver. Invece che chiamano le funzioni di gestione Driver con lo stesso nome e la gestione di Driver chiama le funzioni di driver. In genere, ciò accade quasi immediatamente. Ad esempio, l'applicazione chiama **SQLExecute** in Gestione Driver e dopo alcuni controlli degli errori, gestione Driver chiama **SQLExecute** nel driver.  
  
 Il processo di connessione è diverso. Quando l'applicazione chiama **SQLAllocHandle** con le opzioni su SQL_HANDLE_ENV e SQL_HANDLE_DBC, la funzione consente di allocare gli handle solo in Gestione Driver. Gestione Driver non chiama questa funzione nel driver perché non conoscere il driver da chiamare. Analogamente, se l'applicazione passa l'handle di una connessione non è connessa al **SQLSetConnectAttr** oppure **SQLGetConnectAttr**only the Driver Manager esegue la funzione. Archivia o ottiene il valore dell'attributo dalla connessione all'handle e restituisce SQLSTATE 08003 (connessione non aperta) durante il recupero di un valore per un attributo non è stato impostato e per quale ODBC non definisce un valore predefinito.  
  
 Quando l'applicazione chiama **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**, gestione Driver determina innanzitutto quali driver da usare. Quindi una verifica per determinare se un driver è attualmente caricato per la connessione:  
  
-   Se nessun driver viene caricato per la connessione, gestione Driver controlla se il driver specificato viene caricato in un'altra connessione nello stesso ambiente. Se non, gestione Driver viene caricato il driver per la connessione mentre le chiamate **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_ENV.  
  
     The Driver Manager chiamerà **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_DBC o meno è stato appena caricato. Se l'applicazione impostare gli attributi di connessione, the Driver Manager chiamerà **SQLSetConnectAttr** nel driver; se si verifica un errore, la funzione di connessione di gestione Driver restituisce SQLSTATE IM006 (patente  **SQLSetConnectAttr** non riuscita). Infine, gestione Driver chiama la funzione di connessione nel driver.  
  
-   Se viene caricato il driver specificato nella connessione, gestione Driver chiama la funzione di connessione nel driver. In questo caso, il driver deve assicurarsi che tutti gli attributi di connessione per la connessione mantiene le impostazioni correnti.  
  
-   Se viene caricato un driver diverso per la connessione, the Driver Manager chiamerà **SQLFreeHandle** nel driver per liberare la connessione. Se non sono presenti altre connessioni che usano il driver, Driver Manager chiamerà **SQLFreeHandle** nel driver per liberare l'ambiente e scarica il driver. Gestione Driver esegue quindi le stesse operazioni come quando non viene caricato un driver per la connessione.  
  
 Gestione Driver bloccherà l'handle di ambiente (*henv*) prima di chiamare un driver **SQLAllocHandle** e **SQLFreeHandle** quando *HandleType* è impostata su **SQL_HANDLE_DBC**.  
  
 Quando l'applicazione chiama **SQLDisconnect**, le chiamate di gestione Driver **SQLDisconnect** nel driver. Tuttavia, lascia il driver caricato nel caso in cui l'applicazione si riconnette al driver. Quando l'applicazione chiama **SQLFreeHandle** con l'opzione SQL_HANDLE_DBC, gestione Driver chiama **SQLFreeHandle** nel driver. Se il driver non viene utilizzato da altre connessioni, the Driver Manager chiamerà **SQLFreeHandle** nel driver con il SQL_HANDLE_ENV opzione e scarica il driver.
