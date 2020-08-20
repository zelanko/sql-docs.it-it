---
description: Aggiornamento da un driver 3.5 a un driver 3.8
title: Aggiornamento di un driver 3,5 a un driver 3,8 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461333"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Aggiornamento da un driver 3.5 a un driver 3.8
In questo argomento vengono fornite linee guida e considerazioni per l'aggiornamento di un driver ODBC 3,5 a un driver ODBC 3,8.  
  
##### <a name="version-numbers"></a>Numeri di versione  
 Le linee guida seguenti sono correlate ai numeri di versione:  
  
-   Un driver deve supportare SQL_OV_ODBC3_80 per SQL_ATTR_ODBC_VERSION, restituendo SQL_ERROR per i valori diversi da SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80. Nelle versioni future di gestione driver si presuppone che un driver supporti un livello di conformità ODBC se il driver restituisce SQL_SUCCESS dalla [funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Un driver della versione 3,8 deve restituire 03,80 da **SQLGetInfo** quando SQL_DRIVER_ODBC_VER viene passato a *InfoType*. Tuttavia, i responsabili di driver precedenti, inclusi nelle versioni precedenti di Microsoft Windows, considereranno il driver come versione 3,5 e emetteranno un avviso.  
  
     In Windows 7, la versione di gestione driver è 03,80. In Windows 8, la versione di gestione driver è 03,81 tramite il SQL_DM_VER SQLGetInfo (parametro*InfoType* ). SQL_ODBC_VER segnala la versione come 03,80 in Windows 7 e Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipi di dati C specifici del driver  
 Un driver può avere tipi di dati C personalizzati quando funziona con un'applicazione ODBC della versione 3,8. Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md). Tuttavia, non è necessario che un driver 3,8 implementi i tipi C specifici del driver. Tuttavia, il driver deve comunque eseguire la verifica dell'intervallo dei tipi C; Gestione driver non eseguirà questa operazione per i driver 3,8. Per semplificare lo sviluppo di driver, è possibile definire il valore del tipo di dati C specifico del driver nel formato seguente:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi  
 Quando si sviluppa un nuovo driver, è necessario utilizzare l'intervallo specifico del driver per i tipi di dati, i tipi di descrittori, i tipi di informazioni, i tipi di diagnostica e gli attributi. Gli intervalli specifici del driver e i relativi valori del tipo di base vengono descritti in [tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool di connessioni  
 Per una migliore gestione del pool di connessioni, in ODBC 3,8 è stato introdotto l'attributo di connessione SQL_ATTR_RESET_CONNECTION in **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES è l'unico valore valido per questo attributo. SQL_ATTR_RESET_CONNECTION verrà impostato immediatamente prima che Gestione driver collochi una connessione nel pool di connessioni, consentendo al driver di reimpostare i valori predefiniti per gli altri attributi di connessione.  
  
 Per evitare la comunicazione non necessaria con il server, un driver può rinviare la reimpostazione dell'attributo di connessione fino alla successiva comunicazione con il server remoto, dopo che la connessione è stata riutilizzata dal pool.  
  
 Si noti che SQL_ATTR_RESET_CONNECTION viene usato solo nella comunicazione tra Gestione driver e un driver. Un'applicazione non può impostare direttamente questo attributo. Tutti i driver della versione 3,8 devono implementare questo attributo di connessione.  
  
##### <a name="streamed-output-parameters"></a>Parametri di output trasmessi  
 ODBC versione 3,8 introduce parametri di output trasmessi, un modo più scalabile per recuperare i parametri di output. Per ulteriori informazioni, vedere [recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md). Per supportare questa funzionalità, un driver deve impostare SQL_GD_OUTPUT_PARAMS nel valore restituito quando SQL_GETDATA_EXTENSIONS è *InfoType* in una chiamata **SQLGetInfo** . Il supporto per un tipo SQL con i parametri di output trasmessi deve essere implementato nel driver. Gestione driver non genererà un errore per un tipo SQL non valido. I tipi SQL che supportano i parametri di output trasmessi vengono definiti nel driver.  
  
 Un driver deve restituire SQL_ERROR se l'applicazione usa **SQLGetData** per recuperare un parametro che non è uguale al parametro restituito da **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Esecuzione asincrona per le operazioni di connessione (metodo di polling)  
 Un driver può abilitare il supporto asincrono per varie operazioni di connessione.  
  
 A partire da Windows 7, ODBC supporta il metodo di polling (per altre informazioni, vedere [esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Non è necessario che un driver ODBC della versione 3,8 implementi operazioni asincrone sugli handle di connessione. Anche se un driver non implementa operazioni asincrone sugli handle di connessione, il driver deve comunque implementare il SQL_ASYNC_DBC_FUNCTIONS *InfoType* e restituire **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando le operazioni di connessione asincrone sono abilitate, il tempo di esecuzione di un'operazione di connessione è il tempo totale di tutte le chiamate ripetute. Se l'ultima chiamata ripetuta viene eseguita dopo che il tempo totale ha superato il valore impostato dall'attributo di connessione SQL_ATTR_CONNECTION_TIMEOUT e l'operazione non è stata completata, il driver restituisce SQL_ERROR e registra un record di diagnostica con SQLState HYT01 e il messaggio "timeout della connessione scaduto". Non esiste alcun timeout se l'operazione è stata completata.  
  
##### <a name="sqlcancelhandle-function"></a>Funzione SQLCancelHandle  
 ODBC 3,8 supporta la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), utilizzata per annullare le operazioni di connessione e di istruzione. Un driver che supporta **SQLCancelHandle** deve esportare la funzione. Un driver non deve annullare alcuna funzione di connessione sincrona o asincrona in corso se l'applicazione chiama **SQLCancel** o **SQLCancelHandle** in un handle di istruzione. Analogamente, un driver non deve annullare alcuna funzione di istruzione sincrona o asincrona in corso se un'applicazione chiama **SQLCancelHandle** sull'handle di connessione. Inoltre, un driver non deve annullare l'operazione di esplorazione (**SQLBrowseConnect** restituisce SQL_NEED_DATA) se l'applicazione chiama **SQLCancelHandle** nell'handle di connessione. In questi casi, un driver deve restituire HY010, "errore della sequenza di funzioni".  
  
 Non è necessario supportare contemporaneamente le operazioni di connessione **SQLCancelHandle** e asincrona. Un driver può supportare le operazioni di connessione asincrone, ma non **SQLCancelHandle**, o viceversa.  
  
##### <a name="suspended-connections"></a>Connessioni sospese  
 Gestione driver ODBC 3,8 può impostare una connessione nello stato Suspended. Un'applicazione chiamerà **Disconnect** per rilasciare le risorse associate alla connessione. In questo caso, un driver deve tentare di rilasciare il maggior numero possibile di risorse senza verificare lo stato della connessione. Per ulteriori informazioni sullo stato Suspended, vedere [funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
 ODBC in Windows 8 consente ai driver di personalizzare il comportamento del pool di connessioni. Per ulteriori informazioni, vedere [pool di connessioni compatibile](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)con i driver.  
  
##### <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)  
 ODBC 3,8 supporta il metodo di notifica per le operazioni asincrone, disponibile a partire da Windows 8. Per ulteriori informazioni, vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Driver ODBC forniti da Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
