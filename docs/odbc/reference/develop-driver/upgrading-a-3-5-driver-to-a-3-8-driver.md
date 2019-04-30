---
title: L'aggiornamento di un Driver 3.5 a un Driver 3.8 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df2fa8df9af317bd76b2d7f10e50f7cc937e4660
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254162"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Aggiornamento da un driver 3.5 a un driver 3.8
In questo argomento vengono fornite indicazioni e considerazioni sull'aggiornamento di un driver ODBC 3.5 a un driver ODBC 3.8.  
  
##### <a name="version-numbers"></a>Numeri di versione  
 Le linee guida seguenti si riferiscono ai numeri di versione:  
  
-   Un driver deve supportare SQL_OV_ODBC3_80 per SQL_ATTR_ODBC_VERSION, restituzione di SQL_ERROR per valori diversi da SQL_OV_ODBC2 SQL_OV_ODBC3 e SQL_OV_ODBC3_80. Presuppongono che un driver supporta un livello di conformità ODBC se il driver restituisce SQL_SUCCESS da versioni future di gestione Driver [SQLSetEnvAttr-funzione](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Un driver versione 3.8 deve restituire 03.80 dal **SQLGetInfo** quando SQL_DRIVER_ODBC_VER viene passato a *InfoType*. Tuttavia, i responsabili di Driver precedente, incluse nelle versioni precedenti di Microsoft Windows, verrà considera i driver come un driver versione 3.5 ed emette un avviso.  
  
     In Windows 7, la versione di gestione Driver è 03.80. In Windows 8, la versione di gestione Driver è 03.81 tramite il SQL_DM_VER SQLGetInfo (*InfoType* parametro). SQL_ODBC_VER segnala la versione come 03.80 in Windows 7 e Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipi di dati C specifici del driver  
 Un driver può avere personalizzati i tipi di dati C quando si integra con un'applicazione ODBC versione 3.8. (Per altre informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) Tuttavia, non vi è alcun requisito per un driver 3.8 implementare tutti i tipi C specifiche del driver. Ma il driver deve comunque eseguire la verifica dell'intervallo dei tipi di C. Gestione Driver non verrà eseguita che per i 3.8 driver. Per facilitare lo sviluppo di driver, il valore del tipo di dati C specifico, driver può essere definito nel formato seguente:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi  
 Durante lo sviluppo di un nuovo driver, è necessario utilizzare l'intervallo di specifici del driver per i tipi di dati, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi. Gli intervalli specifici del driver e i relativi valori di tipo di base sono descritti [tipi di dati specifici del Driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool di connessioni  
 Per una migliore gestione del pool di connessioni, ODBC 3.8 introduce l'attributo di connessione SQL_ATTR_RESET_CONNECTION nelle **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES è l'unico valore valido per questo attributo. Verrà impostato SQL_ATTR_RESET_CONNECTION appena prima che Gestione Driver imposti una connessione nel pool di connessioni, consentendo al driver reimpostare gli altri attributi di connessione per i relativi valori predefiniti.  
  
 Per evitare comunicazioni non necessarie con il server, un driver può rinviare l'attributo di connessione reimpostato fino alla successiva comunicazione con il server remoto, dopo la connessione viene riutilizzata dal pool.  
  
 Si noti che SQL_ATTR_RESET_CONNECTION viene usata solo in comunicazione tra gestione Driver e un driver. Un'applicazione non è possibile impostare questo attributo direttamente. Tutti i driver di versione 3.8 devono implementare l'attributo di connessione.  
  
##### <a name="streamed-output-parameters"></a>Parametri di Output inviati come flusso  
 ODBC versione 3.8 introduce i parametri di output inviati come flusso, in modo più scalabile per recuperare i parametri di output. (Per altre informazioni, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Per supportare questa funzionalità, un driver necessario impostare SQL_GD_OUTPUT_PARAMS nel valore restituito quando SQL_GETDATA_EXTENSIONS è il *InfoType* in un **SQLGetInfo** chiamare. Supporto per un tipo SQL con parametri flusso di output deve essere implementato nel driver. Gestione Driver non genererà un errore per un tipo SQL non valido. I tipi di SQL che supportano i parametri di output inviati come flusso è definito nel driver.  
  
 Un driver restituisce SQL_ERROR se l'applicazione utilizzata **SQLGetData** per recuperare un parametro che non è quello utilizzato per il parametro restituito da **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Esecuzione asincrona per le operazioni di connessione (metodo di Polling)  
 Un driver è possibile abilitare il supporto asincrono per varie operazioni di connessione.  
  
 A partire da Windows 7, ODBC supporta il metodo di polling (per altre informazioni, vedere [esecuzione asincrona (metodo di Polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Non è necessario per un driver ODBC versione 3.8 implementare operazioni asincrone sugli handle di connessione. Anche se un driver può neimplementuje metodu operazioni asincrone sugli handle di connessione, il driver deve comunque implementare la SQL_ASYNC_DBC_FUNCTIONS *InfoType* e restituire **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando sono abilitate le operazioni di connessione asincrona, il tempo di esecuzione di un'operazione di connessione è il tempo totale di tutte le chiamate ripetute. Se l'ultimo ripetuto chiamata si verifica dopo che il tempo totale ha superato il valore impostato dall'attributo SQL_ATTR_CONNECTION_TIMEOUT connessione e l'operazione non è terminata, il driver restituisce SQL_ERROR e registra un record di diagnostica con SQLState HYT01 e messaggio "timeout della connessione scaduto". Assenza di timeout se l'operazione completata.  
  
##### <a name="sqlcancelhandle-function"></a>Funzione SQLCancelHandle  
 Supporta ODBC 3.8 [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), che consente di annullare le operazioni di connessione e delle istruzioni. Un driver che supporta **SQLCancelHandle** necessario esportare la funzione. Un driver non deve annullare qualsiasi funzione di connessione sincrona o asincrona che è in corso l'applicazione chiama **SQLCancel** oppure **SQLCancelHandle** su un handle di istruzione. Analogamente, un driver non deve annullare qualsiasi funzione istruzione sincrona o asincrona è in corso se un'applicazione chiama **SQLCancelHandle** nell'handle di connessione. Inoltre, un driver non deve annullare l'operazione di navigazione (**SQLBrowseConnect** restituisce SQL_NEED_DATA) se l'applicazione chiama **SQLCancelHandle** nell'handle di connessione. In questi casi, un driver deve restituire HY010, "Errore nella funzione sequenza".  
  
 Non è necessario supportare entrambe **SQLCancelHandle** e le operazioni di connessione asincrona nello stesso momento. Un driver può supportare operazioni di connessione asincrona, ma non **SQLCancelHandle**, o viceversa.  
  
##### <a name="suspended-connections"></a>Connessioni sospese  
 La gestione dei Driver di ODBC 3.8 possibile inserire una connessione in stato sospeso. Un'applicazione chiamerà **SQLDisconnect** per rilasciare le risorse associate alla connessione. In questo caso, un driver deve provare a rilasciare le risorse tanti possibili senza controllare lo stato della connessione. Per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
 ODBC in Windows 8 consente di personalizzare il comportamento del pool di connessioni per i driver. Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)  
 ODBC 3.8 supporta il metodo di notifica per le operazioni asincrone, disponibile a partire da Windows 8. Per altre informazioni, vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Driver ODBC forniti da Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
