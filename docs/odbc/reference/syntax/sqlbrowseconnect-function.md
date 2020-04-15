---
title: 'Funzione SQLBrowseConnect : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301341"
---
# <a name="sqlbrowseconnect-function"></a>Funzione SQLBrowseConnect
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLBrowseConnect** supporta un metodo iterativo per l'individuazione e l'enumerazione degli attributi e dei valori di attributo necessari per connettersi a un'origine dati. Ogni chiamata a **SQLBrowseConnect** restituisce livelli successivi di attributi e valori di attributo. Quando tutti i livelli sono stati enumerati, viene completata una connessione all'origine dati e viene restituita una stringa di connessione completa da **SQLBrowseConnect**. Un codice restituito di SQL_SUCCESS o SQL_SUCCESS_WITH_INFO indica che tutte le informazioni di connessione sono state specificate e che l'applicazione è ora connessa all'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *InConnectionStringInConnectionString (Informazioni in stringa)*  
 [Ingresso] Sfogliare la stringa di connessione della richiesta (vedere *"Argomento InConnectionString"* in "Commenti").  
  
 *LunghezzaStringa1*  
 [Ingresso] Lunghezza di*InConnectionString* in caratteri.  
  
 *Stringa OutConnectionStringOutConnectionString*  
 [Uscita] Puntatore a un buffer di caratteri in cui restituire la stringa di connessione risultato Sfoglia (vedere "*Argomento OutConnectionString"* in "Commenti").  
  
 Se *OutConnectionString* è NULL, *StringLength2Ptr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *OutConnectionString*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza, in caratteri, del buffer*di OutConnectionString.*  
  
 *StringLength2Ptr*  
 [Uscita] Numero totale di caratteri (esclusa la terminazione \*null) disponibili per la restituzione in *OutConnectionString*. Se il numero di caratteri disponibili per la restituzione è \*maggiore o uguale a *BufferLength*, la stringa di connessione in *OutConnectionString* verrà troncata a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBrowseConnect** restituisce SQL_ERROR, SQL_SUCCESS_WITH_INFO o SQL_NEED_DATA, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un *Handle di ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLBrowseConnect** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *OutConnectionString* non era sufficientemente grande per restituire l'intera stringa di connessione del risultato di esplorazione, pertanto la stringa è stata troncata. Il buffer*StringLength2Ptr* contiene la lunghezza della stringa di connessione del risultato di esplorazione non troncato. (Funzione restituisce SQL_NEED_DATA.)|  
|01S00 (inquesto da windows)|Attributo della stringa di connessione non valido|Nella stringa di connessione della richiesta di esplorazione è stata specificata una parola chiave di attributo non valida (*InConnectionString*). (Funzione restituisce SQL_NEED_DATA.)<br /><br /> Nella stringa di connessione della richiesta di esplorazione (*InConnectionString*) è stata specificata una parola chiave di attributo che non si applica al livello di connessione corrente. (Funzione restituisce SQL_NEED_DATA.)|  
|01S02 (in questo stato di|Valore modificato|Il driver non supportava il valore specificato dell'argomento *ValuePtr* in **SQLSetConnectAttr** e ha sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08001|Il client non è in grado di stabilire la connessione|Il driver non è riuscito a stabilire una connessione con l'origine dati.|  
|08002|Nome connessione in uso|(DM) La connessione specificata era già stata utilizzata per stabilire una connessione con un'origine dati e la connessione era aperta.|  
|08004|Il server ha rifiutato la connessione|L'origine dati ha rifiutato l'istituzione della connessione per motivi definiti dall'implementazione.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui il driver stava tentando di connettersi non è riuscito prima del completamento dell'elaborazione della funzione.|  
|28000|Specifica di autorizzazione non valida|L'identificatore utente o la stringa di autorizzazione o entrambi, come specificato nella stringa di connessione della richiesta di esplorazione (*InConnectionString*), ha violato le restrizioni definite dall'origine dati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|(DM) Gestione Driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.<br /><br /> Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|Un'operazione asincrona è stata annullata chiamando la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Quindi, la funzione originale è stata chiamata nuovamente su *ConnectionHandle*.<br /><br /> Un'operazione è stata annullata chiamando **SQLCancelHandle** su *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) una funzione in esecuzione in modo asincrono (non questo) è stato chiamato per il *ConnectionHandle* ed era ancora in esecuzione quando questa funzione è stata chiamata.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *StringLength1* è minore di 0 e non è uguale a SQL_NTS.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength* è minore di 0.|  
|HY114|Driver non supporta l'esecuzione di funzioni asincrone a livello di connessioneDriver does not support connection level asynchronous function execution|(DM) L'applicazione ha abilitato l'operazione asincrona sull'handle di connessione prima di effettuare la connessione. Tuttavia, il driver non supporta l'operazione asincrona sull'handle di connessione.|  
|HYT00|Timeout|Il periodo di timeout di accesso è scaduto prima del completamento della connessione all'origine dati. Il periodo di timeout viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver corrispondente al nome dell'origine dati specificato non supporta la funzione.|  
|IM002 (in vi eim.|Origine dati non trovata e nessun driver predefinito specificato|(DM) Il nome dell'origine dati specificato nella stringa di connessione della richiesta Sfoglia (*InConnectionString*) non è stato trovato nelle informazioni di sistema, né è stata trovata una specifica del driver predefinita.<br /><br /> (DM) Impossibile trovare l'origine dati ODBC e le informazioni sul driver predefinito nelle informazioni di sistema.|  
|IM003|Impossibile caricare il driver specificato|(DM) Il driver elencato nella specifica dell'origine dati nelle informazioni di sistema o specificato dalla parola chiave **DRIVER** non è stato trovato o non può essere caricato per altri motivi.|  
|IM004|**SQLAllocHandle** del driver in SQL_HANDLE _ENV non riuscita|(DM) durante **SQLBrowseConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *HandleType* di SQL_HANDLE_ENV e il driver ha restituito un errore.|  
|IM005|**SQLAllocHandle** del driver in SQL_HANDLE_DBC non riuscita|(DM) durante **SQLBrowseConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *HandleType* di SQL_HANDLE_DBC e il driver ha restituito un errore.|  
|IM006|**SQLSetConnectAttr** del driver non riuscito|(DM) durante **SQLBrowseConnect**, Gestione Driver ha chiamato la funzione **SQLSetConnectAttr** del driver e il driver ha restituito un errore.|  
|IM009 (invii di iMSM)|Impossibile caricare la DLL di conversione|Il driver non è riuscito a caricare la DLL di conversione specificata per l'origine dati o per la connessione.|  
|IM010 (invii di iMSM)|Nome dell'origine dati troppo lungoData source name too long|(DM) il valore dell'attributo per la parola chiave DSN era più lungo di SQL_MAX_DSN_LENGTH caratteri.|  
|IM011|Nome del driver troppo lungo|(DM) il valore dell'attributo per la parola chiave DRIVER era più lungo di 255 caratteri.|  
|IM012 (invii di iMS12)|Errore di sintassi della parola chiave DRIVER|(DM) La coppia parola chiave-valore per la parola chiave DRIVER conteneva un errore di sintassi.|  
|IM014 (invii di iMs)|Il DSN specificato contiene una mancata corrispondenza dell'architettura tra il driver e l'applicazione|(DM) applicazione a 32 bit utilizza un DSN di connessione a un driver a 64 bit; o viceversa.|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
|S1118 (informazioni in due)|Driver non supporta la notifica asincrona|Quando il driver non supporta la notifica asincrona, non è possibile impostare SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argomento InConnectionString  
 Una stringa di connessione richiesta Sfoglia ha la sintassi seguente:A browse request connection string has the following syntax:  
  
 *stringa di connessione* ::`;`attributo [ ] *attributo*&#124; *attributo* `;` *stringa di connessione*;<br>
 *attributo* :: *: attributo-parolachiave-valore-attributo*`=`*attribute-value* &#124; `DRIVER=`[`{`]*valore-attributo*[`}`]<br>
 *parola chiave-attributo* `DSN` `UID` :: &#124; &#124; `PWD` &#124; *parola chiave dell'attributo definito dal driver*<br>
 *valore-attributo* :: *stringa di caratteri*<br>
 *driver-defined-attribute-keyword* :: *identificatore*<br>
  
 dove *stringa-carattere* ha zero o più caratteri; *identificatore* ha uno o più caratteri; *attribute-keyword* non fa distinzione tra maiuscole e minuscole; *attribute-value* può fare distinzione tra maiuscole e minuscole; e il valore della parola chiave **DSN** non è costituito esclusivamente da spazi vuoti. A causa della stringa di connessione e della grammatica del file di inizializzazione, le parole chiave e i valori degli attributi che contengono i caratteri **[),;?{} \*Evitare** . A causa della grammatica nelle informazioni di sistema, le parole\\chiave e i nomi delle origini dati non possono contenere il carattere barra rovesciata ( ). Per un ODBC 2. *x* driver, le parentesi graffe sono necessarie intorno al valore dell'attributo per la parola chiave DRIVER.  
  
 Se le parole chiave vengono ripetute nella stringa di connessione della richiesta sfoglia, il driver utilizza il valore associato alla prima occorrenza della parola chiave. Se le parole chiave **DSN** e **DRIVER** sono incluse nella stessa stringa di connessione richiesta Sfoglia, Gestione Driver e driver utilizzano qualsiasi parola chiave viene visualizzata per prima.  
  
 Per informazioni su come un'applicazione sceglie un'origine dati o un driver, vedere [Scelta di un'origine dati o di un driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argomento OutConnectionString  
 La stringa di connessione del risultato di esplorazione è un elenco di attributi di connessione. Un attributo di connessione è costituito da una parola chiave di attributo e da un valore di attributo corrispondente. La stringa di connessione del risultato sfoglia ha la sintassi seguente:The browse result connection string has the following syntax:  
  
 *stringa di connessione* ::`;` *attributo*[ ] &#124; stringa di *connessione* *dell'attributo* `;`<br>
 *attributo* ::`*`: [ ]*attributo-parola-valore*`=`*attributo*<br>
 *parola chiave-attributo* :: : *ODBC-attributo-parola* chiave &#124; *driver-defined-attribute-keyword*<br>
 *LA parola chiave (ODBC-attribute-keyword)* -`UID` &#124; (&#124; `PWD``:`- 9*localized-identifier*] *driver-defined-attribute-keyword* :: : *identifier*[`:`*localized-identifier*] *attribute-value* :: s `{` *attribute-value-list* `}` &#124; `?` (le parentesi graffe sono letterali; vengono restituite dal driver).<br>
 *attributo-valore-elenco* :: *stringa-carattere* `:`[ stringa di caratteri`:`*localizzati*] &#124; stringa di *caratteri* [*stringa di caratteri localizzati*] `,` *attributo-valore-elenco*<br>
  
 dove *stringa di caratteri* e stringa di caratteri *localizzati* hanno zero o più caratteri; *identifier* e *localized-identifier* hanno uno o più caratteri; *attribute-keyword* non fa distinzione tra maiuscole e minuscole; e *attribute-value* può essere tra maiuscole e minuscole. A causa della grammatica della stringa di connessione e del file di inizializzazione, delle parole chiave, degli identificatori localizzati e dei valori degli attributi che contengono i caratteri **[]{}(),;? \*Evitare** . A causa della grammatica nelle informazioni di sistema, le parole\\chiave e i nomi delle origini dati non possono contenere il carattere barra rovesciata ( ).  
  
 La sintassi della stringa di connessione del risultato Sfoglia viene utilizzata in base alle regole semantiche seguenti:The browse result connection string syntax is used according to the following semantic rules:  
  
-   Se un\*asterisco ( ) precede una *parola chiave di attributo*, l'attributo è facoltativo e può essere omesso nella chiamata successiva a **SQLBrowseConnect**. *attribute*  
  
-   Le parole chiave dell'attributo **UID** e **PWD** hanno lo stesso significato definito in **SQLDriverConnect**.  
  
-   Un *driver-defined-attribute-keyword* denomina il tipo di attributo per il quale può essere fornito un valore di attributo. Ad esempio, potrebbe essere **SERVER**, **DATABASE**, **HOST**o **DBMS**.  
  
-   *ODBC-attribute-keywords* e *driver-defined-attribute-keywords* includono una versione localizzata o intuitiva della parola chiave. Questo potrebbe essere utilizzato dalle applicazioni come etichetta in una finestra di dialogo. Tuttavia, **UID**, **PWD**o l'identificatore da solo deve essere utilizzato quando si passa una stringa di richiesta Sfoglia al driver. *identifier*  
  
-   *L'attributo-valore-list*è un'enumerazione di valori effettivi validi per la *parola chiave dell'attributo*corrispondente. Si noti che{}le parentesi graffe ( ) non indicano un elenco di scelte; vengono restituiti dal conducente. Ad esempio, potrebbe essere un elenco di nomi di server o un elenco di nomi di database.  
  
-   Se il *valore dell'attributo* è un singolo punto interrogativo (?), un singolo valore corrisponde alla *parola chiave attribute*. Ad esempio, UID-JohnS; PWD-Sesamo.  
  
-   Ogni chiamata a **SQLBrowseConnect** restituisce solo le informazioni necessarie per soddisfare il livello successivo del processo di connessione. Il driver associa le informazioni sullo stato all'handle di connessione in modo che il contesto possa sempre essere determinato a ogni chiamata.  
  
## <a name="using-sqlbrowseconnect"></a>Utilizzo di SQLBrowseConnectUsing SQLBrowseConnect  
 **SQLBrowseConnect** richiede una connessione allocata. Gestione Driver carica il driver specificato in o che corrisponde al nome dell'origine dati specificato nella stringa di connessione richiesta di esplorazione iniziale; per informazioni su quando ciò si verifica, vedere la sezione "Commenti" in [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Il driver può stabilire una connessione con l'origine dati durante il processo di esplorazione. Se **SQLBrowseConnect** restituisce SQL_ERROR, le connessioni in sospeso vengono terminate e la connessione viene restituita a uno stato non connesso.  
  
> [!NOTE]  
>  **SQLBrowseConnect** non supporta il pool di connessioni. Se **SQLBrowseConnect** viene chiamato mentre il pool di connessioni è abilitato, verrà restituito SQLSTATE HY000 (errore generale).  
  
 Quando **SQLBrowseConnect** viene chiamato per la prima volta su una connessione, la stringa di connessione richiesta Sfoglia deve contenere la parola chiave **DSN** o la parola chiave **DRIVER.** Se la stringa di connessione richiesta Sfoglia contiene la parola chiave **DSN,** Gestione Driver individua una specifica dell'origine dati corrispondente nelle informazioni di sistema:  
  
-   Se Gestione Driver trova la specifica dell'origine dati corrispondente, carica la DLL del driver associato; il driver può recuperare informazioni sull'origine dati dalle informazioni di sistema.  
  
-   Se Gestione Driver non riesce a trovare la specifica dell'origine dati corrispondente, individua la specifica dell'origine dati predefinita e carica la DLL del driver associato; il driver può recuperare informazioni sull'origine dati predefinita dalle informazioni di sistema. "DEFAULT" viene passato al driver per il DSN.  
  
-   Se Gestione Driver non riesce a trovare la specifica dell'origine dati corrispondente e non esiste alcuna specifica dell'origine dati predefinita, restituisce SQL_ERROR con SQLSTATE IM002 (origine dati non trovata e nessun driver predefinito specificato).  
  
 Se la stringa di connessione richiesta Sfoglia contiene la parola chiave **DRIVER,** Gestione Driver carica il driver specificato; non tenta di individuare un'origine dati nelle informazioni di sistema. Poiché la parola chiave **DRIVER** non utilizza informazioni dalle informazioni di sistema, il driver deve definire parole chiave sufficienti in modo che un driver possa connettersi a un'origine dati utilizzando solo le informazioni nelle stringhe di connessione della richiesta di esplorazione.  
  
 A ogni chiamata a **SQLBrowseConnect**, l'applicazione specifica i valori degli attributi di connessione nella stringa di connessione della richiesta di esplorazione. Il driver restituisce livelli successivi di attributi e valori di attributo nella stringa di connessione risultato Sfoglia; restituisce SQL_NEED_DATA finché sono presenti attributi di connessione che non sono ancora stati enumerati nella stringa di connessione richiesta sfoglia. L'applicazione utilizza il contenuto della stringa di connessione del risultato Sfoglia per compilare la stringa di connessione della richiesta di esplorazione per la chiamata successiva a **SQLBrowseConnect**. Tutti gli attributi obbligatori (quelli non preceduti da un asterisco nell'argomento *OutConnectionString)* devono essere inclusi nella chiamata successiva a **SQLBrowseConnect**. Si noti che l'applicazione non può utilizzare il contenuto delle stringhe di connessione risultato Sfoglia precedenti durante la compilazione della stringa di connessione richiesta Sfoglia corrente; ovvero non può specificare valori diversi per gli attributi impostati nei livelli precedenti.  
  
 Quando tutti i livelli di connessione e gli attributi associati sono stati enumerati, il driver restituisce SQL_SUCCESS, la connessione all'origine dati è completa e una stringa di connessione completa viene restituita all'applicazione. La stringa di connessione è adatta per l'utilizzo, insieme a **SQLDriverConnect**, con l'opzione SQL_DRIVER_NOPROMPT per stabilire un'altra connessione. La stringa di connessione completa non può essere utilizzata in un'altra chiamata a **SQLBrowseConnect**, tuttavia; se **SQLBrowseConnect** venisse chiamato di nuovo, l'intera sequenza di chiamate dovrebbe essere ripetuta.  
  
 **SQLBrowseConnect** restituisce anche SQL_NEED_DATA se sono presenti errori recuperabili e non irreversibili durante il processo di esplorazione; ad esempio, una password non valida o una parola chiave di attributo fornita dall'applicazione. Quando viene restituito SQL_NEED_DATA e la stringa di connessione risultato Sfoglia non viene modificata, si è verificato un errore e l'applicazione può chiamare **SQLGetDiagRec** per restituire SQLSTATE per gli errori di esplorazione. Ciò consente all'applicazione di correggere l'attributo e continuare la ricerca.  
  
 Un'applicazione può terminare il processo di esplorazione in qualsiasi momento chiamando **SQLDisconnect**. Il driver terminerà tutte le connessioni in sospeso e restituirà la connessione a uno stato non connesso.  
  
 Se le operazioni asincrone sono abilitate sull'handle di connessione, **SQLBrowseConnect** potrebbe restituire anche SQL_STILL_EXECUTING. Quando restituisce SQL_NEED_DATA, un'applicazione deve utilizzare **SQLDisconnect** per annullare il processo di esplorazione. Se **SQLBrowseConnect** restituisce SQL_STILL_EXECUTING, un'applicazione deve utilizzare **SQLCancelHandle** per annullare l'operazione in corso. La chiamata a **SQLCancelHandle** dopo che la funzione restituisce SQL_NEED_DATA non ha alcun effetto.  
  
 Per ulteriori informazioni, vedere [Connessione con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Se un driver supporta **SQLBrowseConnect**, la sezione relativa alla parola chiave del driver nelle informazioni di sistema per il driver deve contenere la parola chiave **ConnectFunctions** con il terzo set di caratteri "Y".  
  
## <a name="code-example"></a>Esempio di codice  
  
> [!NOTE]  
>  Se ci si connette a un provider di origini `Trusted_Connection=yes` dati che supporta l'autenticazione di Windows, è necessario specificare al posto delle informazioni relative all'ID utente e alla password nella stringa di connessione.  
  
 Nell'esempio seguente, un'applicazione chiama **SQLBrowseConnect** ripetutamente. Ogni volta che **SQLBrowseConnect** restituisce SQL_NEED_DATA, restituisce \*le informazioni sui dati necessari in *OutConnectionString*. L'applicazione passa *OutConnectionString* alla routine **GetUserInput** (non illustrato). **GetUserInput** analizza le informazioni, compila e visualizza una finestra di dialogo \*e restituisce le informazioni immesse dall'utente in *InConnectionString*. L'applicazione passa le informazioni dell'utente al driver nella chiamata successiva a **SQLBrowseConnect**. Dopo che l'applicazione ha fornito tutte le informazioni necessarie per la connessione del driver all'origine dati, **SQLBrowseConnect** restituisce SQL_SUCCESS e l'applicazione procede.  
  
 Per un esempio più dettagliato di connessione a un driver di SQL Server chiamando **SQLBrowseConnect**, vedere Esempio di [esplorazione di SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Ad esempio, per connettersi all'origine dati Sales, potrebbero verificarsi le azioni seguenti. In primo luogo, l'applicazione passa la stringa seguente a **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 Gestione Driver carica il driver associato all'origine dati Sales. Chiama quindi la funzione **SQLBrowseConnect** del driver con gli stessi argomenti ricevuti dall'applicazione. Il driver restituisce la stringa riportata di seguito in *:*  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 L'applicazione passa questa stringa alla routine **GetUserInput,** che crea una finestra di dialogo che chiede all'utente di selezionare il server rosso, blu o verde e di immettere un ID utente e una password. La routine restituisce le seguenti \*informazioni specificate dall'utente in *InConnectionString*, che l'applicazione passa a **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** utilizza queste informazioni per connettersi al server rosso come Smith con la password Sesame e quindi restituisce la stringa seguente in*OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 L'applicazione passa questa stringa alla routine **GetUserInput,** che compila una finestra di dialogo che richiede all'utente di selezionare un database. L'utente seleziona empdata e l'applicazione chiama SQLBrowseConnect un'ultima volta con questa stringa:The user selects empdata and the application calls **SQLBrowseConnect** a final time with this string:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Questa è l'ultima informazione di cui il driver ha bisogno per connettersi all'origine dati. **SQLBrowseConnect** restituisce SQL_SUCCESS, e*OutConnectionString* contiene la stringa di connessione completata:  
  
```cpp  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia di connessione|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnectSQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Disconnessione da un'origine datiDisconnecting from a data source|[Funzione SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituzione delle descrizioni e degli attributi dei driver|[Funzione SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberare un handle di connessione|[SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
