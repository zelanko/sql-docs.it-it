---
title: 'Funzione SQLConnect : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301217"
---
# <a name="sqlconnect-function"></a>Funzione SQLConnect
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLConnect** stabilisce le connessioni a un driver e a un'origine dati. L'handle di connessione fa riferimento all'archiviazione di tutte le informazioni sulla connessione all'origine dati, inclusi lo stato, lo stato della transazione e le informazioni sull'errore.  
  
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
 [Ingresso] Nome dell'origine dati. I dati potrebbero trovarsi sullo stesso computer del programma o su un altro computer da qualche parte in una rete. Per informazioni sulla scelta di un'origine dati da parte di un'applicazione, vedere [Scelta di un'origine dati o](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)di un driver .  
  
 *NameLength1*  
 [Ingresso] Lunghezza di :*NomeServer* in caratteri.  
  
 *Nome utente*  
 [Ingresso] Identificatore utente.  
  
 *NameLength2*  
 [Ingresso] Lunghezza di :*UserName* in caratteri.  
  
 *autenticazione*  
 [Ingresso] Stringa di autenticazione (in genere la password).  
  
 *NameLength3*  
 [Ingresso] Lunghezza*dell'autenticazione* in caratteri.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConnect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_DBC e un *handle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLConnect** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Il driver non supportava il valore specificato dell'argomento *ValuePtr* in **SQLSetConnectAttr** e ha sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08001|Il client non è in grado di stabilire la connessione|Il driver non è riuscito a stabilire una connessione con l'origine dati.|  
|08002|Nome connessione in uso|(DM) *L'oggetto specificato ConnectionHandle* era già stato utilizzato per stabilire una connessione con un'origine dati e la connessione era ancora aperta o l'utente stava cercando una connessione.|  
|08004|Il server ha rifiutato la connessione|L'origine dati ha rifiutato l'istituzione della connessione per motivi definiti dall'implementazione.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui il driver stava tentando di connettersi non è riuscito prima che la funzione completasse l'elaborazione.|  
|28000|Specifica di autorizzazione non valida|Il valore specificato per l'argomento *UserName* o il valore specificato per l'argomento *Authentication* ha violato le restrizioni definite dall'origine dati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|(DM) Gestione Driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *ConnectionHandle*. La funzione **SQLConnect** è stata chiamata e prima del completamento dell'esecuzione, la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) è stata chiamata su *ConnectionHandle*, quindi la funzione **SQLConnect** è stata chiamata nuovamente su *ConnectionHandle*.<br /><br /> In alternativa, è stata chiamata la funzione **SQLConnect** e prima del completamento dell'esecuzione, **SQLCancelHandle** è stato chiamato su *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *ConnectionHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *NameLength1*, *NameLength2*o *NameLength3* è minore di 0 ma non uguale a SQL_NTS.<br /><br /> (DM) Il valore specificato per l'argomento *NameLength1* ha superato la lunghezza massima per il nome di un'origine dati.|  
|HYT00|Timeout|Il periodo di timeout della query è scaduto prima del completamento della connessione all'origine dati. Il periodo di timeout viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HY114|Driver non supporta l'esecuzione di funzioni asincrone a livello di connessioneDriver does not support connection level asynchronous function execution|(DM) L'applicazione ha abilitato l'operazione asincrona sull'handle di connessione prima di effettuare la connessione. Tuttavia, il driver non supporta le operazioni asincrone sull'handle di connessione.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) il driver specificato dal nome dell'origine dati non supporta la funzione.|  
|IM002 (in vi eim.|Origine dati non trovata e nessun driver predefinito specificato|(DM) Il nome dell'origine dati specificato nell'argomento *NomeServer* non è stato trovato nelle informazioni di sistema, né è stata trovata una specifica del driver predefinita.|  
|IM003|Impossibile collegare il driver specificato|(DM) Il driver elencato nella specifica dell'origine dati nelle informazioni di sistema non è stato trovato o non è stato in grado di essere connesso per altri motivi.|  
|IM004|SQLAllocHandle del driver su SQL_HANDLE_ENV non riuscita|(DM) durante **SQLConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *HandleType* di SQL_HANDLE_ENV e il driver ha restituito un errore.|  
|IM005|SQLAllocHandle del driver in SQL_HANDLE_DBC non riuscita|(DM) durante **SQLConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *HandleType* di SQL_HANDLE_DBC e il driver ha restituito un errore.|  
|IM006|SQLSetConnectAttr del driver non riuscito|Durante **SQLConnect**, Gestione Driver chiamato il driver **SQLSetConnectAttr** funzione e il driver ha restituito un errore. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|IM009 (invii di iMSM)|Impossibile connettersi alla DLL di conversione|Il driver non è riuscito a connettersi alla DLL di conversione specificata per l'origine dati.|  
|IM010 (invii di iMSM)|Nome dell'origine dati troppo lungoData source name too long|(DM) * \*NomeServer* era più lungo di SQL_MAX_DSN_LENGTH caratteri.|  
|IM014 (invii di iMs)|Il DSN specificato contiene una mancata corrispondenza dell'architettura tra il driver e l'applicazione|(DM) applicazione a 32 bit utilizza un DSN di connessione a un driver a 64 bit; o viceversa.|  
|IM015 (in vi eim.|SQLConnect del driver in SQL_HANDLE_DBC_INFO_HANDLE non riuscito|Se un driver restituisce SQL_ERROR, Gestione Driver restituirà SQL_ERROR all'applicazione e la connessione avrà esito negativo.<br /><br /> Per ulteriori informazioni su SQL_HANDLE_DBC_INFO_TOKEN, vedere Sviluppo del [riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
|S1118 (informazioni in due)|Driver non supporta la notifica asincrona|Quando il driver non supporta la notifica asincrona, non è possibile impostare SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Commenti  
 Per informazioni sul motivo per cui un'applicazione utilizza **SQLConnect**, vedere [Connessione con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md).  
  
 Gestione Driver non si connette a un driver fino a quando l'applicazione non chiama una funzione (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**) per connettersi al driver . Fino a quel momento, Gestione Driver funziona con i propri handle e gestisce le informazioni di connessione. Quando l'applicazione chiama una funzione di connessione, Gestione Driver controlla se un driver è attualmente connesso per l'oggetto specificato *ConnectionHandle*:  
  
-   Se un driver non è connesso, Gestione Driver si connette al driver e chiama **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV, **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC, **SQLSetConnectAttr** (se l'applicazione ha specificato eventuali attributi di connessione) e la funzione di connessione nel driver. Gestione Driver restituisce SQLSTATE IM006 **(Driver SQLSetConnectOption** non riuscita) e SQL_SUCCESS_WITH_INFO per la funzione di connessione se il driver ha restituito un errore per **SQLSetConnectAttr**. Per ulteriori informazioni, vedere [Connessione a un'origine dati o](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)a un driver .  
  
-   Se il driver specificato è già connesso a *ConnectionHandle*, Gestione Driver chiama solo la funzione di connessione nel driver. In questo caso, il driver deve assicurarsi che tutti gli attributi di connessione per il *ConnectionHandle* mantenere le impostazioni correnti.  
  
-   Se è connesso un driver diverso, Gestione Driver chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC e quindi, se nessun altro driver è connesso a in tale ambiente, chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_ENV nel driver connesso e quindi disconnette il driver. Esegue quindi le stesse operazioni di quando un driver non è connesso.  
  
 Il driver alloca quindi gli handle e si inizializza.  
  
 Quando l'applicazione chiama **SQLDisconnect**, Gestione Driver chiama **SQLDisconnect** nel driver. Tuttavia, non scollega il driver. In questo modo il driver viene in memoria per le applicazioni che si connettono e si disconnettono ripetutamente da un'origine dati. Quando l'applicazione chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC, Gestione Driver chiama **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_DBC e quindi **SQLFreeHandle** con un *HandleType* di SQL_HANDLE_ENV nel driver e quindi disconnette il driver.  
  
 Un'applicazione ODBC può stabilire più di una connessione.  
  
## <a name="driver-manager-guidelines"></a>Linee guida per Gestione driver  
 Il contenuto di*ServerName* influisce sul modo in cui Gestione Driver e un driver collaborano per stabilire una connessione a un'origine dati.  
  
-   Se \* *ServerName* contiene un nome di origine dati valido, Gestione Driver individua la specifica dell'origine dati corrispondente nelle informazioni di sistema e si connette al driver associato. Gestione Driver passa ogni **SQLConnect** argomento al driver.  
  
-   Se non è possibile trovare il nome dell'origine dati o *ServerName* è un puntatore null, Gestione Driver individua la specifica dell'origine dati predefinita e si connette al driver associato. Gestione Driver passa al driver gli argomenti *UserName* e *Authentication* senza modifiche e "DEFAULT" per il *ServerName* argomento.  
  
-   Se l'argomento *ServerName* è "DEFAULT", Gestione Driver individua la specifica dell'origine dati predefinita e si connette al driver associato. Gestione Driver passa ogni **SQLConnect** argomento al driver.  
  
-   Se non è possibile trovare il nome dell'origine dati o *ServerName* è un puntatore null e la specifica dell'origine dati predefinita non esiste, Gestione Driver restituisce SQL_ERROR con SQLSTATE IM002 (nome origine dati non trovato e nessun driver predefinito specificato).  
  
 Dopo essere stato connesso da Gestione Driver, un driver può individuare la specifica dell'origine dati corrispondente nelle informazioni di sistema e utilizzare le informazioni specifiche del driver dalla specifica per completare il set di informazioni di connessione necessarie.  
  
 Se nelle informazioni di sistema per l'origine dati viene specificata una libreria di traduzione predefinita, il driver si connette ad essa. È possibile connettere una libreria di traduzione diversa chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_LIB. Un'opzione di conversione può essere specificata chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_OPTION.  
  
 Se un driver supporta **SQLConnect**, la sezione della parola chiave del driver delle informazioni di sistema per il driver deve contenere la parola chiave **ConnectFunctions** con il primo set di caratteri su "Y".  
  
### <a name="connection-pooling"></a>Pool di connessioni  
 Il pool di connessioni consente a un'applicazione di riutilizzare una connessione già creata. Quando il pool di connessioni è abilitato e **SQLConnect** viene chiamato, Gestione Driver tenta di effettuare la connessione utilizzando una connessione che fa parte di un pool di connessioni in un ambiente che è stato designato per il pool di connessioni. Questo ambiente è un ambiente condiviso utilizzato da tutte le applicazioni che utilizzano le connessioni nel pool.  
  
 Il pool di connessioni viene abilitato prima dell'allocazione dell'ambiente chiamando **SQLSetEnvAttr** per impostare SQL_ATTR_CONNECTION_POOLING su SQL_CP_ONE_PER_DRIVER (che specifica un massimo di un pool per driver) o SQL_CP_ONE_PER_HENV (che specifica un massimo di un pool per ambiente). **SQLSetEnvAttr** in questo caso viene chiamato con *EnvironmentHandle* impostato su null, che rende l'attributo un attributo a livello di processo. Se SQL_ATTR_CONNECTION_POOLING è impostato su SQL_CP_OFF, il pool di connessioni è disabilitato.  
  
 Dopo aver abilitato il pool di connessioni, **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV viene chiamato per allocare un ambiente. L'ambiente allocato da questa chiamata è un ambiente condiviso perché il pool di connessioni è stato abilitato. Tuttavia, l'ambiente che verrà utilizzato non viene determinato fino a quando **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC viene chiamato.  
  
 **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC viene chiamato per allocare una connessione. Gestione Driver tenta di trovare un ambiente condiviso esistente che corrisponde agli attributi di ambiente impostati dall'applicazione. Se tale ambiente non esiste, ne viene creato uno come *ambiente condiviso implicito.* Se viene trovato un ambiente condiviso corrispondente, l'handle di ambiente viene restituito all'applicazione e il relativo conteggio dei riferimenti viene incrementato.  
  
 Tuttavia, la connessione che verrà utilizzata non viene determinata fino a quando non viene chiamato SQLConnect.However, the connection that will be used is not determined until **SQLConnect** is called. A questo punto, Gestione Driver tenta di trovare una connessione esistente nel pool di connessioni che corrisponde ai criteri richiesti dall'applicazione. Questi criteri includono le opzioni di connessione richieste nella chiamata a **SQLConnect** (i valori delle parole chiave *ServerName*, *UserName*e *Authentication)* e tutti gli attributi di connessione impostati dopo **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_DBC è stato chiamato. Gestione Driver controlla questi criteri rispetto alle parole chiave di connessione corrispondente e gli attributi nelle connessioni nel pool. Se viene trovata una corrispondenza, viene utilizzata la connessione nel pool. Se non viene trovata alcuna corrispondenza, viene creata una nuova connessione.  
  
 Se l'attributo SQL_ATTR_CP_MATCH environment è impostato su SQL_CP_STRICT_MATCH, la corrispondenza deve essere esatta per poter utilizzare una connessione nel pool. Se l'attributo di ambiente SQL_ATTR_CP_MATCH è impostato su SQL_CP_RELAXED_MATCH, le opzioni di connessione nella chiamata a **SQLConnect** devono corrispondere, ma non tutti gli attributi di connessione devono corrispondere.  
  
 Le regole seguenti vengono applicate quando un attributo di connessione, come impostato dall'applicazione prima che venga chiamato **SQLConnect,** non corrisponde all'attributo di connessione della connessione nel pool:  
  
-   Se l'attributo di connessione deve essere impostato prima che venga stabilita la connessione:  
  
     Se SQL_ATTR_CP_MATCH è SQL_CP_STRICT_MATCH, SQL_ATTR_PACKET_SIZE nella connessione in pool deve essere identico all'attributo impostato dall'applicazione. Se SQL_CP_RELAXED_MATCH, i valori di SQL_ATTR_PACKET_SIZE possono essere diversi.  
  
     Il valore di SQL_ATTR_LOGIN_VALUE non influisce sulla corrispondenza.  
  
-   Se l'attributo di connessione può essere impostato prima o dopo la connessione:  
  
     Se l'attributo di connessione non è stato impostato dall'applicazione ma è stato impostato sulla connessione nel pool ed è presente un valore predefinito, l'attributo di connessione nella connessione in pool viene impostato come predefinito e viene dichiarata una corrispondenza. Se non è presente alcun valore predefinito, la connessione in pool non viene considerata una corrispondenza.  
  
     Se l'attributo di connessione è stato impostato dall'applicazione ma non è stato impostato sulla connessione nel pool, l'attributo di connessione nel pool viene modificato in quello impostato dall'applicazione e viene dichiarata una corrispondenza.  
  
     Se l'attributo di connessione è stato impostato dall'applicazione ed è stato impostato anche sulla connessione nel pool, ma i valori sono diversi, viene utilizzato il valore dell'attributo di connessione dell'applicazione e viene dichiarata una corrispondenza.  
  
-   Se i valori degli attributi di connessione specifici del driver non sono identici e SQL_ATTR_CP_MATCH è impostata su SQL_CP_STRICT_MATCH, la connessione nel pool non viene utilizzata.  
  
 Quando l'applicazione chiama **SQLDisconnect** per disconnettersi, la connessione viene restituita al pool di connessioni ed è disponibile per il riutilizzo.  
  
### <a name="optimizing-connection-pooling-performance"></a>Ottimizzazione delle prestazioni del pool di connessioniOptimizing Connection Pooling Performance  
 Quando sono coinvolte transazioni distribuite, è possibile ottimizzare le prestazioni del pool di connessioni utilizzando **SQL_DTC_TRANSITION_COST**, ovvero una maschera di bit SQLUINTEGER. Le transizioni a cui si fa riferimento sono le transizioni dell'attributo di connessione SQL_ATTR_ENLIST_IN_DTC passando dal valore 0 a un valore diverso da zero e viceversa. Si tratta di una connessione che passa da non inserito in una transazione distribuita ad inserita in una transazione distribuita e viceversa. A seconda di come il driver ha implementato l'elenco (impostazione dell'attributo di connessione SQL_ATTR_ENLIST_IN_DTC), queste transizioni possono essere costose e pertanto devono essere evitate per ottenere prestazioni ottimali.  
  
 Il valore restituito dal driver contiene qualsiasi combinazione dei bit seguenti:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**, se impostata, implica che la transizione da zero a diverso da zero è significativamente più costosa di una transizione da diverso da zero a un altro valore diverso da zero (inserimento di una connessione precedentemente integrata nella transazione successiva).  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**, se impostata, implica che la transizione da zero a zero è significativamente più costosa rispetto all'utilizzo di una connessione il cui attributo SQL_ATTR_ENLIST_IN_DTC è già impostato su zero.  
  
 Esiste un compromesso tra prestazioni e utilizzo delle connessioni. Se un driver indica che una o più di queste transizioni sono costose, il pool di connessioni della gestione driver risponde mantenendo più connessioni nel pool. Alcune delle connessioni nel pool sono preferite per l'utilizzo non transazionale, altre per l'utilizzo transazionale. Tuttavia, se il driver indica che queste transizioni non sono costose, è possibile utilizzare un numero inferiore di connessioni, ad esempio alternando l'uso non transazionale e quello transazionale.  
  
 I driver che non supportano SQL_ATTR_ENLIST_IN_DTC non devono supportare SQL_DTC_TRANSITION_COST. Per i driver che supportano SQL_ATTR_ENLIST_IN_DTC ma non SQL_DTC_TRANSITION_COST, si presuppone che le transizioni non siano costose, come se il driver restituisse 0 (nessun bit impostato) per questo valore.  
  
 Anche se SQL_DTC_TRANSITION_COST è stato introdotto in ODBC 3.5, un ODBC 2. *x* driver può anche supportarlo perché il gestore di driver eseguirà una query su queste informazioni indipendentemente dalla versione del driver.  
  
### <a name="code-example"></a>Esempio di codice  
 Nell'esempio seguente, un'applicazione alloca l'ambiente e gli handle di connessione. Si connette quindi all'origine dati SalesOrders con l'ID utente JohnS e la password Sesame ed elabora i dati. Al termine dell'elaborazione dei dati, questi si disconnettono dall'origine dati e liberano gli handle.  
  
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
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Individuazione ed enumerazione dei valori necessari per connettersi a un'origine datiDiscovering and enumerating values required to connect to a data source|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Disconnessione da un'origine datiDisconnecting from a data source|[Funzione SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
