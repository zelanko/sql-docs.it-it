---
title: Gestione Driver&#39;s Ruolo nel processo di connessione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305802"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Gestione Driver&#39;s ruolo nel processo di connessione
Tenere presente che le applicazioni non chiamano direttamente le funzioni del driver. Al contrario, chiamano le funzioni di Gestione Driver con lo stesso nome e Gestione Driver chiama le funzioni del driver. Di solito, questo accade quasi immediatamente. Ad esempio, l'applicazione chiama **SQLExecute** in Gestione Driver e dopo alcuni controlli degli errori, Gestione Driver chiama **SQLExecute** nel driver.  
  
 Il processo di connessione è diverso. Quando l'applicazione chiama **SQLAllocHandle** con le opzioni SQL_HANDLE_ENV e SQL_HANDLE_DBC, la funzione alloca gli handle solo in Gestione Driver. Gestione Driver non chiama questa funzione nel driver perché non sa quale driver chiamare. Analogamente, se l'applicazione passa l'handle di una connessione non connessa a **SQLSetConnectAttr** o **SQLGetConnectAttr**, solo Gestione Driver esegue la funzione. Archivia o ottiene il valore dell'attributo dall'handle di connessione e restituisce SQLSTATE 08003 (connessione non aperta) quando si ottiene un valore per un attributo che non è stato impostato e per il quale ODBC non definisce un valore predefinito.  
  
 Quando l'applicazione chiama **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**, Gestione Driver determina innanzitutto il driver da utilizzare. Verifica quindi se un driver è attualmente caricato sulla connessione:  
  
-   Se sulla connessione non viene caricato alcun driver, Gestione Driver controlla se il driver specificato viene caricato su un'altra connessione nello stesso ambiente. In caso contrario, Gestione Driver carica il driver sulla connessione e chiama **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_ENV.  
  
     Gestione Driver chiama quindi **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_DBC, indipendentemente dal fatto che sia stato appena caricato. Se l'applicazione imposta gli attributi di connessione, Gestione Driver chiama **SQLSetConnectAttr** nel driver; se si verifica un errore, la funzione di connessione di Gestione Driver restituisce SQLSTATE IM006 **(SQLSetConnectAttr** del driver non riuscito). Infine, Gestione Driver chiama la funzione di connessione nel driver.  
  
-   Se il driver specificato viene caricato sulla connessione, Gestione Driver chiama solo la funzione di connessione nel driver. In questo caso, il driver deve assicurarsi che tutti gli attributi di connessione sulla connessione mantengano le impostazioni correnti.  
  
-   Se alla connessione viene caricato un driver diverso, Gestione Driver chiama **SQLFreeHandle** nel driver per liberare la connessione. Se non sono presenti altre connessioni che utilizzano il driver, Gestione Driver chiama **SQLFreeHandle** nel driver per liberare l'ambiente e scarica il driver. Gestione Driver esegue quindi le stesse operazioni come quando un driver non è caricato sulla connessione.  
  
 Gestione Driver bloccherà l'handle di ambiente (*henv*) prima di chiamare **SQLAllocHandle** e **SQLFreeHandle** di un driver quando *HandleType* è impostato su **SQL_HANDLE_DBC**.  
  
 Quando l'applicazione chiama **SQLDisconnect**, Gestione Driver chiama **SQLDisconnect** nel driver. Tuttavia, lascia il driver caricato nel caso in cui l'applicazione si riconnette al driver. Quando l'applicazione chiama **SQLFreeHandle** con l'opzione SQL_HANDLE_DBC, Gestione Driver chiama **SQLFreeHandle** nel driver. Se il driver non viene utilizzato da altre connessioni, Gestione Driver chiama **quindi SQLFreeHandle** nel driver con l'opzione SQL_HANDLE_ENV e scarica il driver.
