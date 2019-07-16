---
title: Funzione SQLBrowseConnect | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2960c42690a9528763321bc882bb788b437cb66a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036205"
---
# <a name="sqlbrowseconnect-function"></a>Funzione SQLBrowseConnect
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLBrowseConnect** supporta un metodo iterativo di individuazione e l'enumerazione di attributi e valori di attributo necessari per connettersi a un'origine dati. Ogni chiamata a **SQLBrowseConnect** restituisce livelli successivi di attributi e valori di attributo. Quando sono stati enumerati tutti i livelli, una connessione all'origine dati è stata completata e viene restituita una stringa di connessione completa da **SQLBrowseConnect**. Un codice restituito di SQL_SUCCESS_WITH_INFO o SQL_SUCCESS indica che sono state specificate tutte le informazioni di connessione e l'applicazione è ora connesso all'origine dati.  
  
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
  
 *InConnectionString*  
 [Input] Passare la stringa di connessione richiesta (vedere "*InConnectionString* argomento" in "Commenti").  
  
 *StringLength1*  
 [Input] Lunghezza di **InConnectionString* in caratteri.  
  
 *OutConnectionString*  
 [Output] Puntatore a un buffer di caratteri in cui restituire la stringa di connessione del risultato esplorazione (vedere "*OutConnectionString* argomento" in "Commenti").  
  
 Se *OutConnectionString* sia impostato su NULL *StringLength2Ptr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta *OutConnectionString*.  
  
 *BufferLength*  
 [Input] Lunghezza, espressa in caratteri, del **OutConnectionString* buffer.  
  
 *StringLength2Ptr*  
 [Output] Il numero totale di caratteri (ad eccezione di terminazione null) disponibili per restituire \* *OutConnectionString*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength*, la stringa di connessione in \* *OutConnectionString* viene troncato a  *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NEED_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLBrowseConnect** restituisce SQL_ERROR, SQL_SUCCESS_WITH_INFO o SQL_NEED_DATA, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_STMT e una *Handle di ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLBrowseConnect** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|Il buffer \* *OutConnectionString* non sia abbastanza grande per restituire la stringa di connessione del risultato intero Sfoglia, pertanto la stringa è stata troncata. Il buffer **StringLength2Ptr* contiene la lunghezza della stringa di connessione di risultato non troncato Sfoglia. (Funzione restituisce SQL_NEED_DATA).|  
|01S00|Attributo della stringa di connessione non è valido|È stata specificata una parola chiave di attributo non valido nella stringa di connessione richiesta Sfoglia (*InConnectionString*). (Funzione restituisce SQL_NEED_DATA).<br /><br /> Una parola chiave di attributo è stata specificata nella stringa di connessione richiesta Sfoglia (*InConnectionString*) che non si applica a livello di connessione corrente. (Funzione restituisce SQL_NEED_DATA).|  
|01S02|Valore modificato|Il driver non supportava il valore specificato per il *ValuePtr* argomento nella **SQLSetConnectAttr** e sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08001|Impossibile stabilire la connessione client|Il driver non è riuscito a stabilire una connessione con l'origine dati.|  
|08002|Nome della connessione in uso|(DM) la connessione specificata è già stata utilizzata per stabilire una connessione a un'origine dati e la connessione era aperta.|  
|08004|Il server ha rifiutato la connessione|L'origine dati ha rifiutato la creazione di una connessione per i motivi definiti dall'implementazione.|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato effettuato un tentativo di connessione il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|28000|Specifica di autorizzazione non valido|L'identificatore utente o la stringa di autorizzazione o entrambe, come specificato nella finestra Sfoglia richiesta stringa di connessione (*InConnectionString*), violati restrizioni definite dall'origine dati.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|(DM) The Driver Manager: Impossibile allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.<br /><br /> Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|È stata annullata un'operazione asincrona chiamando [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md). Quindi, la funzione originale è stata chiamata nuovamente nel *ConnectionHandle*.<br /><br /> Un'operazione è stata annullata chiamando **SQLCancelHandle** nel *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *StringLength1* era minore di 0 e non è uguale a SQL_NTS.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength* era minore di 0.|  
|HY114|Driver non supporta l'esecuzione di funzione asincrona a livello di connessione|(DM) l'applicazione è abilitata l'operazione asincrona nell'handle di connessione prima di effettuare la connessione. Tuttavia, il driver non supporta operazione asincrona su handle di connessione.|  
|HYT00|Timeout|Il periodo di timeout di accesso è scaduto prima della connessione all'origine dati completata. Il periodo di timeout viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente al nome dell'origine dati specificata non supporta la funzione.|  
|IM002|Origine dati non trovato e un driver predefinito non specificato|Nome specificato nella stringa di connessione richiesta di esplorazione dell'origine dati (DM) (*InConnectionString*) non è stato trovato nelle informazioni di sistema, né era presente una specifica del driver predefinite.<br /><br /> (DM) ODBC data source e l'impostazione predefinita le informazioni sul driver non è stati trovati nelle informazioni di sistema.|  
|IM003|Non è stato possibile caricare il driver specificato|(DM) il driver elencate nella specifica dell'origine dati le informazioni di sistema o specificato per il **DRIVER** parola chiave non è stato trovato o non può essere caricato per altri motivi.|  
|IM004|Patente **SQLAllocHandle** sul valore di SQL_HANDLE _ENV non è riuscita|(DM) durante **SQLBrowseConnect**, gestione Driver denominato il driver **SQLAllocHandle** utilizzabile con un *HandleType* SQL_HANDLE_ENV e il driver ha restituito un errore.|  
|IM005|Patente **SQLAllocHandle** su SQL_HANDLE_DBC non è riuscita|(DM) durante **SQLBrowseConnect**, gestione Driver denominato il driver **SQLAllocHandle** utilizzabile con un *HandleType* SQL_HANDLE_DBC e il driver ha restituito un errore.|  
|IM006|Patente **SQLSetConnectAttr** non è riuscita|(DM) durante **SQLBrowseConnect**, gestione Driver denominato il driver **SQLSetConnectAttr** (funzione) e il driver ha restituito un errore.|  
|IM009|Impossibile caricare la DLL di conversione|Il driver non è riuscito a caricare la DLL che è stata specificata per l'origine dati o per la connessione di conversione.|  
|IM010|Nome dell'origine dati troppo lungo|(DM) il valore dell'attributo per la parola chiave DSN è più lungo di SQL_MAX_DSN_LENGTH caratteri.|  
|IM011|Nome del driver troppo lungo|(DM) il valore dell'attributo per la parola chiave DRIVER era più di 255 caratteri.|  
|IM012|Errore di sintassi della parola chiave DRIVER|(DM) la coppia parola chiave / valore per la parola chiave DRIVER contenuti di un errore di sintassi.|  
|IM014|Il DSN specificato contiene una mancata corrispondenza architettura tra Driver e applicazioni|Applicazione a 32 bit (DM) usa un DSN che ci si connette a un driver a 64 bit; o viceversa.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
|S1118|Driver non supporta la notifica asincrona|Quando il driver non supporta la notifica asincrona, è possibile impostare SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="inconnectionstring-argument"></a>Argomento InConnectionString  
 Una stringa di connessione richiesta Sfoglia presenta la sintassi seguente:  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*;<br>
 *attribute* ::= *attribute-keyword*`=`*attribute-value* &#124; `DRIVER=`[`{`]*attribute-value*[`}`]<br>
 *attribute-keyword* ::= `DSN` &#124; `UID` &#124; `PWD` &#124; *driver-defined-attribute-keyword*<br>
 *valore dell'attributo* :: = *stringhe di caratteri*<br>
 *definito dall'attributo-parola chiave driver* :: = *identificatore*<br>
  
 in cui *stringhe di caratteri* contiene zero o più caratteri; *identificatore* ha uno o più caratteri; *parola chiave di attributo* non distinzione maiuscole/minuscole; *-valore dell'attributo* potrebbe essere distinzione maiuscole/minuscole; e il valore della **DSN** parola chiave composto unicamente da spazi vuoti. A causa di connessione valori stringa e l'inizializzazione file grammatica, parole chiave e attributi che contengono i caratteri **[]{}(),? \*=! @** deve essere evitata. A causa di grammatica nelle informazioni di sistema, i nomi delle origini dati e le parole chiave non può contenere la barra rovesciata (\\) caratteri. Per un database ODBC 2. *x* driver, è necessario racchiudere il valore dell'attributo per la parola chiave DRIVER tra parentesi graffe.  
  
 Se tutte le parole chiave vengono ripetute nella stringa di connessione richiesta Sfoglia, il driver Usa il valore associato alla prima occorrenza della parola chiave. Se il **DSN** e **DRIVER** parole chiave sono inclusi nella stessa stringa di connessione richiesta Sfoglia, il gestore dei Driver e il driver Usa la parola chiave che viene visualizzata per prima.  
  
 Per informazioni sulla modalità con cui un'applicazione sceglie un'origine dati o driver, vedere [scelta di un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
## <a name="outconnectionstring-argument"></a>Argomento OutConnectionString  
 La stringa di connessione Sfoglia risultato è un elenco di attributi di connessione. Un attributo di connessione è costituita da una parola chiave di attributo e un valore di attributo corrispondente. La stringa di connessione del risultato esplorazione presenta la sintassi seguente:  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*<br>
 *attribute* ::= [`*`]*attribute-keyword*`=`*attribute-value*<br>
 *attribute-keyword* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *Parola chiave di attributo ODBC* = {`UID` &#124; `PWD`} [`:`*localizzato dall'identificatore*] *-definito dall'attributo-parola chiave driver* :: = *identifier*[`:`*localizzato dall'identificatore*] *attributo-valore* :: = `{` *attributo-valore dall'elenco* `}` &#124; `?` (Le parentesi graffe sono valori letterali, vengono restituiti dal driver).<br>
 *attribute-value-list* ::= *character-string* [`:`*localized-character string*] &#124; *character-string* [`:`*localized-character string*] `,` *attribute-value-list*<br>
  
 in cui *stringhe di caratteri* e *stringa di caratteri localizzati* avere zero o più caratteri; *identifier* e *localizzato dall'identificatore* hanno uno o più caratteri; *parola chiave di attributo* non distinzione maiuscole/minuscole; e *attributo-valore* potrebbe essere distinzione maiuscole/minuscole. A causa di connessione stringa di inizializzazione file grammatica, parole chiave, identificatori localizzati e i valori che contengono i caratteri dell'attributo **[]{}(),? \*=! @** deve essere evitata. A causa di grammatica nelle informazioni di sistema, i nomi delle origini dati e le parole chiave non può contenere la barra rovesciata (\\) caratteri.  
  
 Viene utilizzata la sintassi della stringa di connessione risultato Sfoglia secondo le regole semantiche seguenti:  
  
-   Se un asterisco (\*) precede un' *parola chiave di attributo*, il *attributo* è facoltativo e può essere omesso nella chiamata successiva al **SQLBrowseConnect**.  
  
-   Le parole chiave di attributo **UID** e **PWD** hanno lo stesso significato come definito nella **SQLDriverConnect**.  
  
-   Oggetto *-definito dall'attributo-parola chiave driver* denomina il tipo di attributo per cui può essere fornito un valore di attributo. Ad esempio, potrebbe essere **SERVER**, **DATABASE**, **HOST**, oppure **DBMS**.  
  
-   *Parole chiave di attributo ODBC* e *driver--attributo-parole chiave definite* includono una versione localizzata o intuitiva della parola chiave. Ciò potrebbe essere utilizzato da applicazioni come un'etichetta in una finestra di dialogo. Tuttavia **UID**, **PWD**, o la *identificatore* da solo quando è necessario utilizzare passando una stringa di richiesta di esplorazione al driver.  
  
-   La {*attributo-valore-list*} è un'enumerazione dei valori effettivi valido per il corrispondente *parola chiave di attributo*. Si noti che le parentesi graffe ({}) non indicano un elenco di scelte; tali elementi vengono restituiti dal driver. Ad esempio, potrebbe essere un elenco di nomi di server o un elenco di nomi di database.  
  
-   Se il *attributo-valore* è un singolo punto interrogativo (?), un singolo valore corrispondente per il *parola chiave di attributo*. Ad esempio, UID = JohnS; PWD = Sesame.  
  
-   Ogni chiamata a **SQLBrowseConnect** restituisce solo le informazioni necessarie per soddisfare il livello successivo del processo di connessione. Il driver associa le informazioni sullo stato con l'handle di connessione in modo che il contesto può sempre determinato per ogni chiamata.  
  
## <a name="using-sqlbrowseconnect"></a>Con SQLBrowseConnect  
 **SQLBrowseConnect** richiede una connessione allocata. Gestione Driver viene caricato il driver in cui è stato specificato o che corrisponde al nome origine dati specificato nella stringa di connessione richiesta iniziale Sfoglia; Per informazioni su quando ciò si verifica, vedere la sezione "Commenti" nella [funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Il driver può stabilire una connessione con l'origine dati durante il processo di esplorazione. Se **SQLBrowseConnect** restituisce SQL_ERROR, in attesa di connessioni vengono terminate e viene restituita la connessione a uno stato non connesso.  
  
> [!NOTE]  
>  **SQLBrowseConnect** non supporta il pool di connessioni. Se **SQLBrowseConnect** viene chiamato mentre il pool di connessioni è abilitato, SQLSTATE HY000 verrà restituito (errore generale).  
  
 Quando **SQLBrowseConnect** viene chiamato per la prima volta in una connessione, la stringa di connessione richiesta di ricerca deve contenere il **DSN** parola chiave o il **DRIVER** (parola chiave). Se la stringa di connessione richiesta Sfoglia contiene il **DSN** (parola chiave), gestione Driver individua una specifica origine dati corrispondente nelle informazioni di sistema:  
  
-   Se Gestione Driver rileva specifica dell'origine dati corrispondente, viene caricato il driver associato DLL; il driver può recuperare informazioni sull'origine dati dalle informazioni di sistema.  
  
-   Se Gestione Driver non è possibile trovare la specifica origine dati corrispondente, viene individuato specifica dell'origine dati predefinito e carica il driver associato DLL. il driver può recuperare informazioni sull'origine dati predefinita dalle informazioni di sistema. "DEFAULT" viene passato al driver per il DSN.  
  
-   Se Gestione Driver non è possibile trovare una specifica origine dati corrispondente e non esiste alcuna specifica di origine dati predefinita, viene restituito SQL_ERROR con SQLSTATE IM002 (origine dati non trovata e driver predefinito non specificato).  
  
 Se la stringa di connessione richiesta Sfoglia contiene il **DRIVER** (parola chiave), gestione Driver viene caricato il driver specificato; non tenta di individuare un'origine dati le informazioni di sistema. Poiché il **DRIVER** parola chiave non utilizza informazioni dalle informazioni di sistema, il driver deve definire sufficiente parole chiave in modo che un driver può connettersi a un'origine dati usando solo le informazioni nelle stringhe di connessione richiesta Sfoglia.  
  
 In ogni chiamata a **SQLBrowseConnect**, l'applicazione specifica i valori di attributo di connessione nella stringa di connessione richiesta Sfoglia. Il driver restituisce livelli successivi degli attributi e valori degli attributi nella stringa di connessione risultato Sfoglia; restituisce SQL_NEED_DATA, purché siano presenti gli attributi di connessione che non sono ancora stati enumerati nella stringa di connessione richiesta Sfoglia. L'applicazione usa il contenuto della stringa di connessione risultati esplorazione per compilare la stringa di connessione richiesta Sfoglia per la chiamata successiva a **SQLBrowseConnect**. Tutti gli attributi obbligatori (quelle non preceduto da un asterisco nel *OutConnectionString* argomento) devono essere inclusi nella chiamata successiva a **SQLBrowseConnect**. Si noti che l'applicazione non è possibile usare il contenuto delle stringhe di connessione risultato ricerca precedente quando si compila la stringa di connessione richiesta Sfoglia corrente; vale a dire non deve specificare valori diversi per gli attributi impostati nei livelli precedenti.  
  
 Quando tutti i livelli di connessione e i relativi attributi associati sono stati enumerati, il driver restituisce SQL_SUCCESS, la connessione all'origine dati è stata completata e viene restituita una stringa di connessione completa per l'applicazione. La stringa di connessione è adatta da usare, in combinazione con **SQLDriverConnect**, con l'opzione SQL_DRIVER_NOPROMPT per stabilire un'altra connessione. La stringa di connessione completa non può essere utilizzata in un'altra chiamata a **SQLBrowseConnect**, tuttavia, se **SQLBrowseConnect** venisse chiamata nuovamente, l'intera sequenza di chiamate dovrà essere ripetuta.  
  
 **SQLBrowseConnect** anche viene restituito SQL_NEED_DATA se sono presenti errori non irreversibili, reversibili durante il processo di esplorazione; ad esempio, una password non valida o una parola chiave di attributo fornita dall'applicazione. Quando viene restituito SQL_NEED_DATA e la stringa di connessione del risultato Sfoglia viene modificata, si è verificato un errore e l'applicazione può chiamare **SQLGetDiagRec** per restituire il valore SQLSTATE errori della fase di esplorazione. Ciò consente all'applicazione per correggere l'attributo e continuare l'esplorazione.  
  
 Un'applicazione può terminare il processo di ricerca in qualsiasi momento chiamando **SQLDisconnect**. Il driver terminerà tutte le connessioni in sospeso e restituire la connessione a uno stato non connesso.  
  
 Se nell'handle di connessione, sono abilitate le operazioni asincrone **SQLBrowseConnect** potrebbe restituire anche SQL_STILL_EXECUTING. Quando viene restituito SQL_NEED_DATA, un'applicazione deve utilizzare **SQLDisconnect** per annullare il processo di esplorazione. Se **SQLBrowseConnect** restituisce SQL_STILL_EXECUTING, un'applicazione devono usare **SQLCancelHandle** per annullare l'operazione in corso. La chiamata **SQLCancelHandle** dopo la funzione restituisce SQL_NEED_DATA non ha alcun effetto.  
  
 Per altre informazioni, vedere [connessione con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md).  
  
 Se un driver supporta **SQLBrowseConnect**, la sezione di parola chiave driver nelle informazioni di sistema per il driver deve contenere il **ConnectFunctions** parola chiave with il terzo carattere è impostato su "Y".  
  
## <a name="code-example"></a>Esempio di codice  
  
> [!NOTE]  
>  Se ci si connette a un provider dell'origine dati che supporta l'autenticazione di Windows, è necessario specificare `Trusted_Connection=yes` anziché le informazioni utente di ID e la password nella stringa di connessione.  
  
 Nell'esempio seguente, un'applicazione chiama **SQLBrowseConnect** ripetutamente. Ogni volta che **SQLBrowseConnect** restituisce SQL_NEED_DATA, passa nuovamente le informazioni sui dati di cui ha bisogno in \* *OutConnectionString*. L'applicazione passa *OutConnectionString* alla relativa routine **GetUserInput** (non illustrato). **GetUserInput** analizza le informazioni, compila e visualizza una finestra di dialogo e restituisce le informazioni immesse dall'utente nella \* *InConnectionString*. L'applicazione passa le informazioni dell'utente per il driver nella chiamata successiva al **SQLBrowseConnect**. Dopo l'applicazione ha fornito tutte le informazioni necessarie per connettersi all'origine dati, il driver **SQLBrowseConnect** restituisce SQL_SUCCESS e l'applicazione procede.  
  
 Per un esempio più dettagliato di connessione a un driver di SQL Server tramite la chiamata **SQLBrowseConnect**, vedere [esempio di esplorazione di SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md).  
  
 Ad esempio, per connettersi ai dati di origine cliente, potrebbero verificarsi le azioni seguenti. In primo luogo, l'applicazione passa la stringa seguente per **SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 Gestione Driver viene caricato il driver associato all'origine dati vendite. Chiama quindi il driver **SQLBrowseConnect** canonica con gli stessi argomenti ricevuto dall'applicazione. Il driver restituisce la stringa seguente in **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 L'applicazione passa questa stringa al relativo **GetUserInput** routine, che crea una finestra di dialogo che chiede all'utente di selezionare il server di colore rosso, blu o verde e immettere un ID utente e password. La routine passa le informazioni specificate dall'utente seguente nuovamente \* *InConnectionString*, che l'applicazione passa al **SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** Usa queste informazioni per connettersi al server di colore rosso come Smith con la password Sesame e quindi restituisce la stringa seguente nella **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 L'applicazione passa questa stringa al relativo **GetUserInput** routine, che crea una finestra di dialogo che chiede all'utente di selezionare un database. Il empdata Seleziona utente e l'applicazione chiama **SQLBrowseConnect** un'ultima volta con questa stringa:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 Questo è l'ultima informazione che il driver deve connettersi all'origine dati; **SQLBrowseConnect** restituisce SQL_SUCCESS, e **OutConnectionString* contiene la stringa di connessione completata:  
  
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
|Allocare un handle di connessione|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Disconnessione da un'origine dati|[Funzione SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[Funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituzione di attributi e le descrizioni di driver|[Funzione SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Rilascio di un handle di connessione|[Funzione SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
