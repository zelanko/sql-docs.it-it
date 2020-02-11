---
title: Ruolo di gestione driver&#39;s nel processo di connessione | Microsoft Docs
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
ms.openlocfilehash: fdc7f82059579f23c9a1a1203aee5e45c87693e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046938"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Ruolo di gestione driver&#39;s nel processo di connessione
Tenere presente che le applicazioni non chiamano direttamente le funzioni del driver. Al contrario, chiamano le funzioni di gestione driver con lo stesso nome e gestione driver chiama le funzioni del driver. Questa situazione si verifica in genere quasi immediatamente. Ad esempio, l'applicazione chiama **SQLExecute** in Gestione driver e dopo alcuni controlli degli errori, gestione driver chiama **SQLExecute** nel driver.  
  
 Il processo di connessione è diverso. Quando l'applicazione chiama **SQLAllocHandle** con le opzioni SQL_HANDLE_ENV e SQL_HANDLE_DBC, la funzione alloca gli handle solo in Gestione driver. Gestione driver non chiama questa funzione nel driver perché non conosce il driver da chiamare. Analogamente, se l'applicazione passa l'handle di una connessione non connessa a **SQLSetConnectAttr** o **SQLGetConnectAttr**, solo Gestione driver esegue la funzione. Archivia o ottiene il valore dell'attributo dal relativo handle di connessione e restituisce SQLSTATE 08003 (connessione non aperta) quando si ottiene un valore per un attributo che non è stato impostato e per il quale ODBC non definisce un valore predefinito.  
  
 Quando l'applicazione chiama **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**, gestione driver determina innanzitutto il driver da usare. Consente quindi di verificare se un driver è attualmente caricato nella connessione:  
  
-   Se non viene caricato alcun driver sulla connessione, gestione driver controlla se il driver specificato viene caricato in un'altra connessione nello stesso ambiente. In caso contrario, gestione driver carica il driver sulla connessione e chiama **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_ENV.  
  
     Gestione driver chiama quindi **SQLAllocHandle** nel driver con l'opzione SQL_HANDLE_DBC, indipendentemente dal fatto che sia stato appena caricato. Se l'applicazione imposta gli attributi di connessione, gestione driver chiama **SQLSetConnectAttr** nel driver; Se si verifica un errore, la funzione di connessione di gestione driver restituisce SQLSTATE IM006 (il driver **SQLSetConnectAttr** non è riuscito). Infine, gestione driver chiama la funzione di connessione nel driver.  
  
-   Se il driver specificato viene caricato sulla connessione, gestione driver chiama solo la funzione di connessione nel driver. In questo caso, il driver deve assicurarsi che tutti gli attributi di connessione nella connessione mantengano le impostazioni correnti.  
  
-   Se nella connessione viene caricato un driver diverso, gestione driver chiama **SQLFreeHandle** nel driver per liberare la connessione. Se non sono presenti altre connessioni che usano il driver, gestione driver chiama **SQLFreeHandle** nel driver per liberare l'ambiente e Scarica il driver. Gestione driver esegue quindi le stesse operazioni di quando un driver non viene caricato nella connessione.  
  
 Gestione driver bloccherà l'handle di ambiente (*HENV*) prima di chiamare **SQLAllocHandle** e **SQLFreeHandle** di un driver quando *HandleType* è impostato su **SQL_HANDLE_DBC**.  
  
 Quando l'applicazione chiama **Disconnect**, gestione driver chiama **SQLConnect** nel driver. Tuttavia, lascia il driver caricato nel caso in cui l'applicazione si riconnetta al driver. Quando l'applicazione chiama **SQLFreeHandle** con l'opzione SQL_HANDLE_DBC, gestione driver chiama **SQLFreeHandle** nel driver. Se il driver non viene utilizzato da altre connessioni, gestione driver chiama **SQLFreeHandle** nel driver con l'opzione SQL_HANDLE_ENV e Scarica il driver.
