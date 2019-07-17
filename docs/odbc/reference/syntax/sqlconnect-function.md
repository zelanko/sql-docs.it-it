---
title: Funzione SQLConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1c0b20fed0e6c15fef76b1bcbebc98edd37cfbc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121456"
---
# <a name="sqlconnect-function"></a>Funzione SQLConnect
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLConnect** stabilisce le connessioni a un driver e un'origine dati. L'handle di connessione fa riferimento ad archiviazione di tutte le informazioni sulla connessione all'origine dati, inclusi stato, lo stato della transazione e le informazioni sull'errore.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *ServerName*  
 [Input] Nome dell'origine dati. I dati potrebbero trovarsi nello stesso computer del programma, o in un altro computer in una posizione in una rete. Per informazioni sulla modalità con cui un'applicazione sceglie un'origine dati, vedere [scelta di un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 *NameLength1*  
 [Input] Lunghezza di **ServerName* in caratteri.  
  
 *UserName*  
 [Input] Identificatore dell'utente.  
  
 *NameLength2*  
 [Input] Lunghezza di **UserName* in caratteri.  
  
 *Autenticazione*  
 [Input] Stringa di autenticazione (in genere la password).  
  
 *NameLength3*  
 [Input] Lunghezza di **autenticazione* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConnect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_DBC e un *gestiscono* dei *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLConnect** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore di opzione modificato|Il driver non supportava il valore specificato per il *ValuePtr* argomento nella **SQLSetConnectAttr** e sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08001|Impossibile stabilire la connessione client|Il driver non è riuscito a stabilire una connessione con l'origine dati.|  
|08002|Nome della connessione in uso|(DM) specificato *ConnectionHandle* era già stata utilizzata per stabilire una connessione a un'origine dati e la connessione è stata ancora aperta o l'utente Naviga per una connessione.|  
|08004|Il server ha rifiutato la connessione|L'origine dati ha rifiutato la creazione di una connessione per i motivi definiti dall'implementazione.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato effettuato un tentativo di connessione il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|28000|Specifica di autorizzazione non valido|Il valore specificato per l'argomento *nomeutente* o il valore specificato per l'argomento *autenticazione* violati restrizioni definite dall'origine dati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|(DM) The Driver Manager: Impossibile allocare la memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *ConnectionHandle*. Il **SQLConnect** funzione è stata chiamata e prima esecuzione, completata [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stato chiamato sul *ConnectionHandle*e quindi il **SQLConnect** funzione è stata chiamata nuovamente nel *ConnectionHandle*.<br /><br /> OR, il **SQLConnect** funzione è stata chiamata e prima esecuzione, completata **SQLCancelHandle** è stato chiamato sul *ConnectionHandle* da un thread diverso in un applicazioni multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *NameLength1*, *NameLength2*, o *NameLength3* era minore di 0, ma non è uguale a SQL_NTS.<br /><br /> (DM) il valore specificato per l'argomento *NameLength1* supera la lunghezza massima per un nome dell'origine dati.|  
|HYT00|Timeout|Il periodo di timeout query scaduto prima della connessione all'origine dati completata. Il periodo di timeout viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Driver non supporta l'esecuzione di funzione asincrona a livello di connessione|(DM) l'applicazione è abilitata l'operazione asincrona nell'handle di connessione prima di effettuare la connessione. Tuttavia, il driver non supporta operazioni asincrone nell'handle di connessione.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver specificato dal nome dell'origine dati non supporta la funzione.|  
|IM002|Origine dati non trovato e un driver predefinito non specificato|Nome specificato nell'argomento dell'origine dati (DM) *ServerName* non è stato trovato nelle informazioni di sistema, né era presente una specifica del driver predefinite.|  
|IM003|Il driver specificato potrebbe non essere connesso a|Il driver (DM) elencato nei dati di origine specifica in informazioni di sistema non è stato trovato o non potrebbe essere connessa a per altri motivi.|  
|IM004|Funzione SQLAllocHandle del driver su SQL_HANDLE_ENV non riuscita|(DM) durante **SQLConnect**, gestione Driver denominato il driver **SQLAllocHandle** utilizzabile con un *HandleType* SQL_HANDLE_ENV e il driver ha restituito un errore.|  
|IM005|Funzione SQLAllocHandle del driver su SQL_HANDLE_DBC non riuscita|(DM) durante **SQLConnect**, gestione Driver denominato il driver **SQLAllocHandle** utilizzabile con un *HandleType* SQL_HANDLE_DBC e il driver ha restituito un errore.|  
|IM006|Errore di SQLSetConnectAttr del driver|Durante **SQLConnect**, gestione Driver denominato il driver **SQLSetConnectAttr** (funzione) e il driver ha restituito un errore. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|IM009|Non è possibile connettersi alla DLL di conversione|Il driver non è riuscito a connettersi per la traduzione DLL che è stato specificato per l'origine dati.|  
|IM010|Nome dell'origine dati troppo lungo|(DM)  *\*ServerName* più lungo di caratteri SQL_MAX_DSN_LENGTH.|  
|IM014|Il DSN specificato contiene una mancata corrispondenza architettura tra Driver e applicazioni|Applicazione a 32 bit (DM) usa un DSN che ci si connette a un driver a 64 bit; o viceversa.|  
|IM015|SQLConnect del driver su SQL_HANDLE_DBC_INFO_HANDLE non è riuscita|Se un driver restituisce SQL_ERROR, gestione Driver restituirà SQL_ERROR all'applicazione e la connessione avrà esito negativo.<br /><br /> Per altre informazioni sulle SQL_HANDLE_DBC_INFO_TOKEN, vedere [lo sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
|S1118|Driver non supporta la notifica asincrona|Quando il driver non supporta la notifica asincrona, è possibile impostare SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni sui motivi per cui un'applicazione utilizza **SQLConnect**, vedere [la connessione con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 Gestione Driver non si connette a un driver fino a quando l'applicazione chiama una funzione (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**) per la connessione per il driver. Fino a quel momento, gestione Driver funziona con i proprio handle e gestisce le informazioni di connessione. Quando l'applicazione chiama una funzione di connessione, gestione Driver controlla se un driver è connesso per l'oggetto specificato *ConnectionHandle*:  
  
-   Se un driver non è connesso a, gestione Driver si connette al driver e le chiamate **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV, **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC, **SQLSetConnectAttr** (se l'applicazione eventuali connessione gli attributi specificati) e la funzione di connessione nel driver. Gestione Driver restituisce SQLSTATE IM006 (patente **SQLSetConnectOption** non è riuscito) e SQL_SUCCESS_WITH_INFO per la funzione di connessione se il driver ha restituito un errore per **SQLSetConnectAttr**. Per altre informazioni, vedere [la connessione a un'origine dati o Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md).  
  
-   Se il driver specificato è già connesso a on la *ConnectionHandle*, gestione Driver chiama solo la funzione di connessione nel driver. In questo caso, il driver necessario assicurarsi che tutte le connessioni degli attributi per il *ConnectionHandle* mantenere le impostazioni correnti.  
  
-   Se un altro driver è connesso a, the Driver Manager chiamerà **SQLFreeHandle** con un *HandleType* SQL_HANDLE_DBC, e se nessun altro driver è connesso a in quell'ambiente, viene quindi chiamato **SQLFreeHandle** con un *HandleType* SQL_HANDLE_ENV nel driver connessi e quindi si disconnette tale driver. Esegue quindi le stesse operazioni come quando un driver non è connesso a.  
  
 Quindi, il driver consente di allocare handle e inizializzato.  
  
 Quando l'applicazione chiama **SQLDisconnect**, le chiamate di gestione Driver **SQLDisconnect** nel driver. Tuttavia, non si disconnette il driver. In questo modo il driver in memoria per le applicazioni che si connettono più volte e disconnettersi da un'origine dati. Quando l'applicazione chiama **SQLFreeHandle** con un *HandleType* SQL_HANDLE_DBC, gestione Driver chiama **SQLFreeHandle** con un *HandleType*  SQL_HANDLE_DBC e quindi **SQLFreeHandle** con un *HandleType* SQL_HANDLE_ENV nel driver e quindi si disconnette il driver.  
  
 Un'applicazione ODBC è possibile stabilire più connessioni.  
  
## <a name="driver-manager-guidelines"></a>Linee guida di Gestione driver  
 Il contenuto di **ServerName* influiscono sul modo in cui gestione Driver e un driver collaborano per stabilire una connessione a un'origine dati.  
  
-   Se \* *ServerName* contiene un nome di origine dati valido, gestione Driver individua specifica dell'origine dati corrispondente nelle informazioni di sistema e si connette al driver associato. Gestione Driver passa ognuno **SQLConnect** argomento al driver.  
  
-   Se non viene trovato il nome dell'origine dati oppure *ServerName* è un puntatore null, gestione Driver individua specifica dell'origine dati predefinita e si connette al driver associato. Gestione Driver passa al driver i *UserName* e *autenticazione* argomenti senza modificarli e "DEFAULT" per il *ServerName* argomento.  
  
-   Se il *ServerName* argomento è "DEFAULT", gestione Driver individua specifica dell'origine dati predefinita e si connette al driver associato. Gestione Driver passa ognuno **SQLConnect** argomento al driver.  
  
-   Se non viene trovato il nome dell'origine dati oppure *ServerName* è un puntatore null e il valore predefinito specifica origine dati non esiste, gestione Driver restituisce SQL_ERROR con SQLSTATE IM002 (e origine dati nome non è stato trovato alcun valore predefinito driver specificato).  
  
 Dopo averlo connesso da Gestione Driver, un driver può individuare la specifica origine dati corrispondente nelle informazioni di sistema e usare informazioni specifiche del driver dalla specifica per completare un set di informazioni di connessione necessarie.  
  
 Se una libreria di traduzione predefinita è specificata nelle informazioni di sistema per l'origine dati, il driver si connette a esso. Una libreria di conversione diverse può essere connesse a chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_LIB. Un'opzione di conversione può essere specificata chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se un driver supporta **SQLConnect**, la sezione di parola chiave driver delle informazioni di sistema per il driver deve contenere il **ConnectFunctions** parola chiave con il primo carattere è impostato su "Y".  
  
### <a name="connection-pooling"></a>Pool di connessioni  
 Pool di connessioni consente a riutilizzare una connessione che è già stata creata un'applicazione. Quando il pool di connessioni è abilitato e **SQLConnect** viene chiamato, gestione Driver tenta di stabilire la connessione utilizzando una connessione che fa parte di un pool di connessioni in un ambiente che è stato designato per il pool di connessioni. Questo ambiente è un ambiente condiviso che viene usato da tutte le applicazioni che usano le connessioni nel pool.  
  
 Pool di connessioni viene attivato prima che l'ambiente viene allocata tramite la chiamata **SQLSetEnvAttr** impostare SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER (che consente di specificare un massimo di un pool per ogni driver) o SQL_CP_ONE_PER_HENV (che consente di specificare un massimo di un pool per ogni ambiente). **SQLSetEnvAttr** in questo caso viene chiamato con *EnvironmentHandle* impostate su null, che rende l'attributo di un attributo a livello di processo. Se SQL_ATTR_CONNECTION_POOLING è impostato su SQL_CP_OFF, pool di connessioni è disabilitato.  
  
 Dopo aver abilitato il pool di connessioni, **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV viene chiamata per allocare un ambiente. L'ambiente allocato da questa chiamata è un ambiente condiviso, perché il pool di connessioni è stato abilitato. Tuttavia, l'ambiente che verrà usato viene determinato solo **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC viene chiamato.  
  
 **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC viene chiamata per allocare una connessione. Gestione Driver tenta di trovare un ambiente condiviso esistente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se l'ambiente non esiste, ne viene creata come implicita *ambiente condiviso*. Se viene trovato un ambiente condiviso corrisponda, viene restituito l'handle di ambiente per l'applicazione e il conteggio dei riferimenti viene incrementato.  
  
 Tuttavia, la connessione che verrà usata viene determinata solo **SQLConnect** viene chiamato. A questo punto, gestione Driver tenta di trovare una connessione esistente nel pool di connessioni che corrisponde ai criteri richiesti dall'applicazione. Tali criteri includono le opzioni di connessione richieste nella chiamata a **SQLConnect** (i valori delle *ServerName*, *UserName*, e  *L'autenticazione* parole chiave) e gli attributi di connessione impostata poiché **SQLAllocHandle** con un *HandleType* SQL_HANDLE_DBC è stato chiamato. Gestione Driver controlla questi criteri con le parole chiave di connessione corrispondente e gli attributi nelle connessioni nel pool. Se viene trovata una corrispondenza, viene utilizzata la connessione nel pool. Se viene trovata alcuna corrispondenza, viene creata una nuova connessione.  
  
 Se l'attributo di ambiente SQL_ATTR_CP_MATCH è impostato su SQL_CP_STRICT_MATCH, la corrispondenza deve essere esattamente di una connessione in pool da usare. Se l'attributo di ambiente SQL_ATTR_CP_MATCH è impostato su SQL_CP_RELAXED_MATCH, opzioni di connessione nella chiamata a **SQLConnect** devono corrispondenza ma non tutti gli attributi di connessione deve corrispondere.  
  
 Le regole seguenti vengono applicate quando un attributo di connessione, l'impostazione dell'applicazione prima **SQLConnect** viene chiamato, corrisponde all'attributo di connessione della connessione nel pool:  
  
-   Se l'attributo di connessione deve essere impostato prima che venga effettuata la connessione:  
  
     Se SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE nella connessione in pool devono essere identici per l'attributo impostato dall'applicazione. Se SQL_CP_RELAXED_MATCH, i valori di SQL_ATTR_PACKET_SIZE può essere diverso.  
  
     Il valore di SQL_ATTR_LOGIN_VALUE non influenza la corrispondenza.  
  
-   Se l'attributo di connessione può essere impostato prima o dopo aver stabilita la connessione:  
  
     Se l'attributo di connessione non è stato impostato dall'applicazione, ma è stata impostata per la connessione nel pool e vi è un'impostazione predefinita, l'attributo di connessione della connessione in pool è impostata sul valore predefinito e viene dichiarata una corrispondenza. Se è presente alcun valore predefinito, la connessione in pool non viene considerata una corrispondenza.  
  
     Se l'attributo di connessione è stata impostata dall'applicazione ma non è stato impostato per la connessione nel pool, l'attributo di connessione nel pool viene modificato in tale set dall'applicazione e viene dichiarata una corrispondenza.  
  
     Se l'attributo di connessione è stata impostata dall'applicazione e anche stato impostato per la connessione nel pool, ma i valori sono diversi, viene utilizzato il valore dell'attributo di connessione dell'applicazione e viene dichiarata una corrispondenza.  
  
-   Se i valori degli attributi di connessione specifici del driver non sono identici e SQL_ATTR_CP_MATCH è impostato su SQL_CP_STRICT_MATCH, non verrà usata la connessione nel pool.  
  
 Quando l'applicazione chiama **SQLDisconnect** per disconnettersi, la connessione viene restituita al pool di connessioni ed è disponibile per il riutilizzo.  
  
### <a name="optimizing-connection-pooling-performance"></a>Ottimizzazione delle prestazioni del pool  
 Quando sono coinvolte le transazioni distribuite, è possibile ottimizzare le prestazioni del pool usando **SQL_DTC_TRANSITION_COST**, maschera di bit SQLUINTEGER. Le transizioni definite sono le transizioni dell'attributo di connessione SQL_ATTR_ENLIST_IN_DTC a diverso da zero, il valore 0 e viceversa. Si tratta di una connessione da non integrate in una transazione distribuita integrata in una transazione distribuita e viceversa. A seconda di come il driver ha implementato l'integrazione (attributo di connessione impostazione SQL_ATTR_ENLIST_IN_DTC), queste transizioni possono essere costose e pertanto evitare per ottimizzare le prestazioni.  
  
 Il valore restituito dal driver contiene qualsiasi combinazione dei bit seguenti:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, quando impostato, implica lo zero per la transizione diverso da zero è molto più costoso di una transizione da diverso da zero a un altro valore diverso da zero (integrazione di una connessione già integrata in transazioni successiva).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, quando impostato, implica il diverso da zero a zero transizione è molto più costoso rispetto all'uso di una connessione il cui attributo SQL_ATTR_ENLIST_IN_DTC è già impostato su zero.  
  
 È delle prestazioni rispetto a compromesso di utilizzo di connessione. Se un driver indica che uno o più di queste transizioni sono costose, pool di connessioni di Gestione driver risponde a questa, mantenendo ulteriori connessioni nel pool. Alcune connessioni nel pool sono preferibili per l'uso non transazionale e alcuni sono preferibili per l'uso transazionale. Tuttavia, se il driver indica che queste transizioni non siano onerosi, meno connessioni utilizzabile, alternatamente forse non transazionale e l'uso transazionale.  
  
 I driver che non supportano SQL_ATTR_ENLIST_IN_DTC non sono necessario supportare SQL_DTC_TRANSITION_COST. Per i driver che supportano SQL_ATTR_ENLIST_IN_DTC ma non SQL_DTC_TRANSITION_COST, si presuppone che le transizioni non siano onerosi, come se il driver ha restituito 0 (Nessun set di bit) per questo valore.  
  
 Sebbene SQL_DTC_TRANSITION_COST è stato introdotto in ODBC 3.5, un'API ODBC 2. *x* driver può anche supportarla perché Gestione driver eseguirà una query queste informazioni indipendentemente dalla versione del driver.  
  
### <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione alloca connessione e ambiente gli handle. Quindi si connette all'origine dei dati degli ordini di vendita con l'utente ID JohnS e la password Sesame ed elabora i dati. Dopo aver terminato l'elaborazione dei dati, si disconnette dall'origine dati e consente di liberare l'handle.  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di un handle|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|L'individuazione e l'enumerazione dei valori necessari per connettersi a un'origine dati|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Disconnessione da un'origine dati|[Funzione SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[Funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituisce l'impostazione di un attributo di connessione|[Funzione SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostare un attributo di connessione|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
