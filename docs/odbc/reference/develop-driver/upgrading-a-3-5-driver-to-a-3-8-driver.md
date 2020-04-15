---
title: Aggiornamento di un driver 3.5 a un driver 3.8 Documenti Microsoft
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
ms.openlocfilehash: dcd01d050e806b733d75c54058945d367a33d6a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294432"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Aggiornamento da un driver 3.5 a un driver 3.8
In questo argomento vengono fornite linee guida e considerazioni per l'aggiornamento di un driver ODBC 3.5 a un driver ODBC 3.8.  
  
##### <a name="version-numbers"></a>Numeri di versione  
 Le linee guida seguenti si riferiscono ai numeri di versione:The following guidelines relate to version numbers:  
  
-   Un driver deve supportare SQL_OV_ODBC3_80 per SQL_ATTR_ODBC_VERSION, restituendo SQL_ERROR per valori diversi da SQL_OV_ODBC2, SQL_OV_ODBC3 e SQL_OV_ODBC3_80. Le versioni future di Gestione Driver presupporranno che un driver supporti un livello di conformità ODBC se il driver restituisce SQL_SUCCESS dalla funzione [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Un driver versione 3.8 deve restituire 03.80 da **SQLGetInfo** quando SQL_DRIVER_ODBC_VER viene passato a *InfoType*. Tuttavia, i gestori di driver meno recenti, inclusi nelle versioni precedenti di Microsoft Windows, considereranno il driver come un driver della versione 3.5 e emetteranno un avviso.  
  
     In Windows 7, la versione di Gestione Driver è 03.80. In Windows 8, la versione di Gestione Driver è 03.81 tramite il SQLGetInfo SQL_DM_VER (parametro*InfoType).* SQL_ODBC_VER segnala la versione come 03.80 in Windows 7 e Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Tipi di dati C specifici del driverDriver-Specific C Data Types  
 Un driver può avere tipi di dati C personalizzati quando funziona con un'applicazione ODBC versione 3.8. (Per ulteriori informazioni, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md). Tuttavia, non è necessario per un driver 3.8 per implementare qualsiasi tipo C specifico del driver. Ma il driver dovrebbe ancora eseguire il controllo gamma di tipi C; Gestione Driver non lo farà per i driver 3.8. Per facilitare lo sviluppo del driver, il valore del driver specifico, tipo di dati C può essere definito nel seguente formato:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipi di dati specifici del driver, tipi di descrittore, tipi di informazioni, tipi di diagnostica e attributi  
 Quando si sviluppa un nuovo driver, è necessario utilizzare l'intervallo specifico del driver per i tipi di dati, i tipi di descrittore, i tipi di informazioni, i tipi di diagnostica e gli attributi. Gli intervalli specifici del driver e i relativi valori dei tipi di base sono descritti in Tipi di dati specifici del [driver, Tipi di descrittore, Tipi di informazioni, Tipi di diagnostica e Attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Pool di connessioni  
 Per una migliore gestione del pool di connessioni, ODBC 3.8 introduce l'attributo di connessione SQL_ATTR_RESET_CONNECTION in **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES è l'unico valore valido per questo attributo. SQL_ATTR_RESET_CONNECTION verrà impostata appena prima che Gestione Driver inserisce una connessione nel pool di connessioni, consentendo al driver di reimpostare gli altri attributi di connessione sui valori predefiniti.  
  
 Per evitare comunicazioni non necessarie con il server, un driver può rinviare la reimpostazione dell'attributo di connessione fino alla successiva comunicazione con il server remoto, dopo che la connessione è stata riutilizzata dal pool.  
  
 Si noti che SQL_ATTR_RESET_CONNECTION viene utilizzato solo nelle comunicazioni tra Gestione Driver e un driver. Un'applicazione non può impostare direttamente questo attributo. Tutti i driver della versione 3.8 devono implementare questo attributo di connessione.  
  
##### <a name="streamed-output-parameters"></a>Parametri di output trasmessi  
 ODBC versione 3.8 introduce i parametri di output trasmessi, un modo più scalabile per recuperare i parametri di output. Per altre informazioni, vedere Recupero di parametri di [output tramite SQLGetData.](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md) Per supportare questa funzionalità, un driver deve impostare SQL_GD_OUTPUT_PARAMS nel valore restituito quando SQL_GETDATA_EXTENSIONS è il InfoType in una chiamata **SQLGetInfo.To** support this feature, a driver should set SQL_GD_OUTPUT_PARAMS in the return value when SQL_GETDATA_EXTENSIONS is the *InfoType* in a SQLGetInfo call. Il supporto per un tipo SQL con parametri di output trasmessi deve essere implementato nel driver. Gestione Driver non genererà un errore per un tipo SQL non valido. I tipi SQL che supportano i parametri di output trasmessi sono definiti nel driver.  
  
 Un driver deve restituire SQL_ERROR se l'applicazione ha utilizzato **SQLGetData** per recuperare un parametro diverso da quello restituito da **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Esecuzione asincrona per le operazioni di connessione (metodo polling)Asynchronous Execution for Connection Operations (Polling Method)  
 Un driver può abilitare il supporto asincrono per varie operazioni di connessione.  
  
 A partire da Windows 7, ODBC supporta il metodo di polling (per ulteriori informazioni, vedere [esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Non è necessario che un driver ODBC versione 3.8 implementi operazioni asincrone sugli handle di connessione. Anche se un driver non implementa operazioni asincrone sugli handle di connessione, il driver deve comunque implementare il SQL_ASYNC_DBC_FUNCTIONS *InfoType* e restituire **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Quando le operazioni di connessione asincrone sono abilitate, il tempo di esecuzione di un'operazione di connessione è il tempo totale di tutte le chiamate ripetute. Se l'ultima chiamata ripetuta si verifica dopo che il tempo totale ha superato il valore impostato dall'attributo di connessione SQL_ATTR_CONNECTION_TIMEOUT e l'operazione non è stata completata, il driver restituisce SQL_ERROR e registra un record di diagnostica con SQLState HYT01 e il messaggio "Timeout di connessione scaduto". Non vi è alcun timeout se l'operazione è stata completata.  
  
##### <a name="sqlcancelhandle-function"></a>Funzione SQLCancelHandle  
 ODBC 3.8 supporta la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md), utilizzata per annullare le operazioni di connessione e istruzione. Un driver che supporta **SQLCancelHandle** deve esportare la funzione. Un driver non deve annullare alcuna funzione di connessione sincrona o asincrona in corso se l'applicazione chiama **SQLCancel** o **SQLCancelHandle** su un handle di istruzione. Analogamente, un driver non deve annullare alcuna funzione di istruzione sincrona o asincrona in corso se un'applicazione chiama **SQLCancelHandle** sull'handle di connessione. Inoltre, un driver non deve annullare l'operazione di esplorazione (**SQLBrowseConnect** restituisce SQL_NEED_DATA) se l'applicazione chiama **SQLCancelHandle** sull'handle di connessione. In questi casi, un driver deve restituire HY010, "errore di sequenza di funzione".  
  
 Non è necessario supportare contemporaneamente **sqlCancelHandle** e le operazioni di connessione asincrone. Un driver può supportare operazioni di connessione asincrone ma non **SQLCancelHandle**o viceversa.  
  
##### <a name="suspended-connections"></a>Connessioni sospese  
 Gestione Driver ODBC 3.8 può mettere una connessione in stato sospeso. Un'applicazione chiamerà **SQLDisconnect** per rilasciare le risorse associate alla connessione. In questo caso, un driver deve tentare di rilasciare il maggior numero possibile di risorse senza controllare lo stato della connessione. Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Pool di connessioni compatibile con il driver  
 ODBC in Windows 8 consente ai driver di personalizzare il comportamento del pool di connessioni. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver .  
  
##### <a name="asynchronous-execution-notification-method"></a>Esecuzione asincrona (metodo di notifica)  
 ODBC 3.8 supporta il metodo di notifica per le operazioni asincrone, disponibile a partire da Windows 8. Per ulteriori informazioni, vedere [Esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Driver ODBC forniti da Microsoft](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
