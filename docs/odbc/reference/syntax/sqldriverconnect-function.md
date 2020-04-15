---
title: Funzione SQLDriverConnect . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302772"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect Function
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLDriverConnect** è un'alternativa a **SQLConnect**. Supporta origini dati che richiedono più informazioni di connessione rispetto ai tre argomenti in **SQLConnect**, finestre di dialogo per richiedere all'utente tutte le informazioni di connessione e le origini dati che non sono definite nelle informazioni di sistema.  
  
 **SQLDriverConnect** fornisce i seguenti attributi di connessione:  
  
-   Stabilire una connessione utilizzando una stringa di connessione che contiene il nome dell'origine dati, uno o più ID utente, una o più password e altre informazioni richieste dall'origine dati.  
  
-   Stabilire una connessione utilizzando una stringa di connessione parziale o nessuna informazione aggiuntiva; in questo caso, Gestione Driver e il driver possono richiedere all'utente le informazioni di connessione.  
  
-   Stabilire una connessione a un'origine dati non definita nelle informazioni di sistema. Se l'applicazione fornisce una stringa di connessione parziale, il driver può richiedere all'utente le informazioni di connessione.  
  
-   Stabilire una connessione a un'origine dati utilizzando una stringa di connessione costruita dalle informazioni contenute in un file DSN.  
  
 Dopo aver stabilito una connessione, **SQLDriverConnect** restituisce la stringa di connessione completata. L'applicazione può utilizzare questa stringa per le richieste di connessione successive. Per ulteriori informazioni, vedere [Connessione con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>Argomenti  
 *ConnectionHandle*  
 [Input] Handle di connessione.  
  
 *WindowHandle*  
 [Ingresso] Handle della finestra. L'applicazione può passare l'handle della finestra padre, se applicabile, o un puntatore null se l'handle della finestra non è applicabile o **SQLDriverConnect** non presenterà alcuna finestra di dialogo.  
  
 *InConnectionStringInConnectionString (Informazioni in stringa)*  
 [Ingresso] Stringa di connessione completa (vedere la sintassi in "Commenti"), una stringa di connessione parziale o una stringa vuota.  
  
 *LunghezzaStringa1*  
 [Ingresso] Lunghezza di ,*InConnectionString*, in caratteri se la stringa è Unicode o byte se string è ANSI o DBCS.  
  
 *Stringa OutConnectionStringOutConnectionString*  
 [Uscita] Puntatore a un buffer per la stringa di connessione completata. Una volta stabilita la connessione all'origine dati di destinazione, questo buffer contiene la stringa di connessione completata. Le applicazioni devono allocare almeno 1.024 caratteri per questo buffer.  
  
 Se *OutConnectionString* è NULL, *StringLength2Ptr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *OutConnectionString*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del buffer*Di OutConnectionString,* in caratteri.  
  
 *StringLength2Ptr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *OutConnectionString*. Se il numero di caratteri disponibili per la restituzione è maggiore \*o uguale a *BufferLength*, la stringa di connessione completata in *OutConnectionString* verrà troncata a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
 *Completamento del driver*  
 [Ingresso] Flag che indica se Gestione Driver o il driver deve richiedere ulteriori informazioni sulla connessione:  
  
 SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.  
  
 (Per ulteriori informazioni, vedere "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE o SQL_STILL_EXECUTING.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDriverConnect** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con *un tipo fHandle di* SQL_HANDLE_DBC e un *hHandle* di *ConnectionHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLDriverConnect** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|Il \*buffer *OutConnectionString* non era sufficientemente grande per restituire l'intera stringa di connessione, pertanto la stringa di connessione è stata troncata. La lunghezza della stringa di connessione non troncata viene restituita in *, StringLength2Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S00 (inquesto da windows)|Attributo della stringa di connessione non valido|Nella stringa di connessione è stata specificata una parola chiave di attributo non valida (*InConnectionString*), ma il driver è stato in grado di connettersi comunque all'origine dati. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Il driver non supportava il valore specificato a cui punta l'argomento *ValuePtr* in **SQLSetConnectAttr** e ha sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S08 (in questo)|Errore durante il salvataggio del DSN del file|La stringa in * \*InConnectionString* contiene una parola **chiave FILEDSN,** ma il file DSN non è stato salvato. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S09 (in titolo della ste92):|Parola chiave non valida|(DM) la stringa in * \*InConnectionString* contiene una parola chiave **SAVEFILE** ma non una parola chiave **DRIVER** o **FILEDSN.** (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|08001|Il client non è in grado di stabilire la connessione|Il driver non è riuscito a stabilire una connessione con l'origine dati.|  
|08002|Nome connessione in uso|(DM) *L'oggetto specificato ConnectionHandle* era già stato utilizzato per stabilire una connessione con un'origine dati e la connessione era ancora aperta.|  
|08004|Il server ha rifiutato la connessione|L'origine dati ha rifiutato l'istituzione della connessione per motivi definiti dall'implementazione.|  
|08S01|Errore di collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui il driver stava tentando di connettersi non è riuscito prima che la funzione **SQLDriverConnect** completasse l'elaborazione.|  
|28000|Specifica di autorizzazione non valida|L'identificatore utente o la stringa di autorizzazione o entrambi, come specificato nella stringa di connessione (*InConnectionString*), hanno violato le restrizioni definite dall'origine dati.|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*szMessageText* descrive l'errore e la relativa causa.|  
|HY000|Errore generale: dsn file non valido|(DM) La stringa in*InConnectionString* contiene una parola chiave FILEDSN, ma il nome del file DSN non è stato trovato.|  
|HY000|Errore generale: Impossibile creare il buffer di file|(DM) La stringa in*InConnectionString* contiene una parola chiave FILEDSN, ma il file DSN era illeggibile.|  
|I001|Errore di allocazione della memoria|Gestione Driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione **SQLDriverConnect.**<br /><br /> Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I008|Operation canceled|L'elaborazione asincrona è stata abilitata per *ConnectionHandle*. La funzione è stata chiamata e prima del completamento dell'esecuzione è stata chiamata la [funzione SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) su *ConnectionHandle*, quindi la funzione **SQLDriverConnect** è stata chiamata nuovamente su *ConnectionHandle*.<br /><br /> In alternativa, è stata chiamata la funzione **SQLDriverConnect** e prima del completamento dell'esecuzione, **SQLCancelHandle** è stato chiamato su *ConnectionHandle* da un thread diverso in un'applicazione multithread.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) è stata chiamata un'altra funzione in esecuzione asincrona (non **SQLDriverConnect**) per *ConnectionHandle* ed era ancora in esecuzione quando è stata chiamata la funzione **SQLDriverConnect.**|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata alla funzione **SQLDriverConnect** perché non è stato possibile accedere agli oggetti di memoria sottostanti, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *StringLength1* è minore di 0 e non è uguale a SQL_NTS.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength* è minore di 0.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|(DM) l'argomento *DriverCompletion* è stato SQL_DRIVER_PROMPT e l'argomento *WindowHandle* è un puntatore null.|  
|HY110|Completamento del driver non valido|(DM) il valore specificato per l'argomento *DriverCompletion* non è uguale a SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE, SQL_DRIVER_COMPLETE_REQUIRED o SQL_DRIVER_NOPROMPT.<br /><br /> (DM) Il pool di connessioni è stato abilitato e il valore specificato per l'argomento *DriverCompletion* non è uguale a SQL_DRIVER_NOPROMPT.|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il driver non supporta la versione del comportamento ODBC richiesto dall'applicazione.|  
|HYT00|Timeout|Il periodo di timeout di accesso è scaduto prima del completamento della connessione all'origine dati. Il periodo di timeout viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_LOGIN_TIMEOUT.|  
|HYT01|Timeout connessione scaduto|Il periodo di timeout della connessione è scaduto prima che l'origine dati riscisse risposta alla richiesta. Il periodo di timeout della connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver corrispondente al nome dell'origine dati specificato non supporta la funzione.|  
|IM002 (in vi eim.|Origine dati non trovata e nessun driver predefinito specificato|(DM) Il nome dell'origine dati specificato nella stringa di connessione (*InConnectionString*) non è stato trovato nelle informazioni di sistema e non è presente alcuna specifica del driver predefinito.<br /><br /> (DM) Impossibile trovare l'origine dati ODBC e le informazioni sul driver predefinito nelle informazioni di sistema.|  
|IM003|Impossibile caricare il driver specificato|(DM) Il driver elencato nella specifica dell'origine dati nelle informazioni di sistema o specificato dalla parola chiave **DRIVER** non è stato trovato o non può essere caricato per altri motivi.|  
|IM004|**SQLAllocHandle** del driver su SQL_HANDLE_ENV non riuscito|(DM) durante **SQLDriverConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *fHandleType* di SQL_HANDLE_ENV e il driver ha restituito un errore.|  
|IM005|**SQLAllocHandle** del driver in SQL_HANDLE_DBC non riuscito.|(DM) durante **SQLDriverConnect**, Gestione Driver ha chiamato la funzione **SQLAllocHandle** del driver con un *fHandleType* di SQL_HANDLE_DBC e il driver ha restituito un errore.|  
|IM006|**SQLSetConnectAttr** del driver non riuscito|(DM) durante **SQLDriverConnect**, Gestione Driver ha chiamato la funzione **SQLSetConnectAttr** del driver e il driver ha restituito un errore.|  
|IM007 (invii di iMS77|Nessuna origine dati o driver specificato; finestra di dialogo non consentita|Nessun nome di origine dati o driver è stato specificato nella stringa di connessione e *DriverCompletion* è stato SQL_DRIVER_NOPROMPT.|  
|IM008|Finestra di dialogo non riuscita|Il driver ha tentato di visualizzare la finestra di dialogo di accesso e non è riuscito.<br /><br /> *WindowHandle* era un puntatore null e *DriverCompletion* non era SQL_DRIVER_NO_PROMPT.|  
|IM009 (invii di iMSM)|Impossibile caricare la DLL di conversione|Il driver non è riuscito a caricare la DLL di conversione specificata per l'origine dati o per la connessione.|  
|IM010 (invii di iMSM)|Nome dell'origine dati troppo lungoData source name too long|(DM) il valore dell'attributo per la parola chiave DSN era più lungo di SQL_MAX_DSN_LENGTH caratteri.|  
|IM011|Nome del driver troppo lungo|(DM) il valore dell'attributo per la parola chiave **DRIVER** era più lungo di 255 caratteri.|  
|IM012 (invii di iMS12)|Errore di sintassi della parola chiave DRIVER|(DM) La coppia parola chiave-valore per la parola chiave **DRIVER** conteneva un errore di sintassi.<br /><br /> (DM) la stringa in * \*InConnectionString* contiene una parola **chiave FILEDSN,** ma il file DSN non contiene una parola chiave **DRIVER** o una parola chiave **DSN.**|  
|IM014 (invii di iMs)|Il DSN specificato contiene una mancata corrispondenza dell'architettura tra il driver e l'applicazione|(DM) applicazione a 32 bit utilizza un DSN di connessione a un driver a 64 bit; o viceversa.|  
|IM015 (in vi eim.|SQLDriverConnect del driver in SQL_HANDLE_DBC_INFO_HANDLE non riuscita|Se un driver restituisce SQL_ERROR, Gestione Driver restituirà SQL_ERROR all'applicazione e la connessione avrà esito negativo.<br /><br /> Per ulteriori informazioni su SQL_HANDLE_DBC_INFO_TOKEN, vedere Sviluppo del [riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .|  
|IM017|Il polling è disabilitato in modalità di notifica asincronaPolling is disabled in asynchronous notification mode|Ogni volta che viene utilizzato il modello di notifica, il polling è disabilitato.|  
|IM018 (in vi eim.|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente su questo handle.|Se la chiamata di funzione precedente sull'handle restituisce SQL_STILL_EXECUTING e se la modalità di notifica è abilitata, **SQLCompleteAsync** deve essere chiamato sull'handle per eseguire la post-elaborazione e completare l'operazione.|  
|S1118 (informazioni in due)|Driver non supporta la notifica asincrona|Quando il driver non supporta la notifica asincrona, non è possibile impostare SQL_ATTR_ASYNC_DBC_EVENT o SQL_ATTR_ASYNC_DBC_RETCODE_PTR.|  
  
## <a name="comments"></a>Commenti  
 Una stringa di connessione ha la sintassi seguente:A connection string has the following syntax:  
  
 *stringa di connessione* :: : *stringa vuota*[;] attributo &#124; [;] *attributo*di &#124; ; *attribute* *stringa di connessione*  
  
 *empty-string* ::*: attributo* :: *attributo-parola*=*chiave-valore &#124;* DRIVER [ s]*valore-attributo*[]]  
  
 *parola chiave-attributo* :: : DSN &#124; &#124; PWD &#124; *parola chiave dell'attributo definito dal driver*  
  
 *valore-attributo* :: *stringa di caratteri*  
  
 *driver-defined-attribute-keyword* :: *identificatore*  
  
 dove *stringa-carattere* ha zero o più caratteri; *identificatore* ha uno o più caratteri; *attribute-keyword* non fa distinzione tra maiuscole e minuscole; *attribute-value* può fare distinzione tra maiuscole e minuscole; e il valore della parola chiave **DSN** non è costituito esclusivamente da spazi vuoti.  
  
 A causa della stringa di connessione e della grammatica del file di inizializzazione, le parole chiave e i valori degli attributi che contengono i caratteri **[),;?{} Non \*** racchiudere tra parentesi graffe. Il valore della parola chiave **DSN** non può essere costituito solo da spazi vuoti e non deve contenere spazi vuoti iniziali. A causa della grammatica delle informazioni di sistema, le parole\\chiave e i nomi delle origini dati non possono contenere il carattere barra rovesciata ( ).  
  
 Le applicazioni non devono aggiungere parentesi graffe intorno al valore dell'attributo dopo la parola chiave **DRIVER,** a meno che l'attributo non contenga un punto e virgola (;), nel qual caso le parentesi graffe sono obbligatorie. Se il valore dell'attributo che il driver riceve include parentesi graffe, il driver non deve rimuoverli, ma devono essere parte della stringa di connessione restituita.  
  
 Un DSN o un valore di{}stringa di connessione racchiuso tra parentesi graffe ( ) contenente uno dei caratteri **[]{}(),;? Viene \*** passato intatto al driver. Tuttavia, quando si utilizzano questi caratteri in una parola chiave, Gestione Driver restituisce un errore quando si lavora con DSN di file, ma passa la stringa di connessione al driver per le stringhe di connessione regolari. Evitare di utilizzare parentesi graffe incorporate in un valore di parola chiave.  
  
 La stringa di connessione può includere un numero qualsiasi di parole chiave definite dal driver. Poiché la parola chiave **DRIVER** non utilizza le informazioni delle informazioni di sistema, il driver deve definire parole chiave sufficienti in modo che un driver possa connettersi a un'origine dati utilizzando solo le informazioni nella stringa di connessione. Per ulteriori informazioni, vedere "Linee guida per i driver" più avanti in questa sezione. Il driver definisce quali parole chiave sono necessarie per connettersi all'origine dati.  
  
 Nella tabella seguente vengono descritti i valori degli attributi delle parole **chiave DSN**, **FILEDSN**, **DRIVER**, **UID**, **PWD**e **SAVEFILE** .  
  
|Parola chiave|Descrizione del valore dell'attributo|  
|-------------|---------------------------------|  
|**Dsn**|Nome di un'origine dati restituita da **SQLDataSources** o dalla finestra di dialogo Origini dati di **SQLDriverConnect**.|  
|**FILEDSN (file)**|Nome di un file DSN da cui verrà compilata una stringa di connessione per l'origine dati. Queste origini dati sono denominate origini dati su file.|  
|**autista**|Descrizione del driver restituita dalla funzione **SQLDrivers.** Ad esempio, Rdb o SQL Server.For example, Rdb or SQL Server.|  
|**Uid**|ID utente.|  
|**Pwd**|La password corrispondente all'ID utente o una stringa vuota se non è presente alcuna password per l'ID utente (PWD-;).|  
|**SALVAFILE**|Il nome file di un file DSN in cui devono essere salvati i valori degli attributi delle parole chiave utilizzate per creare la connessione presente e corretta.|  
  
 Per informazioni su come un'applicazione sceglie un'origine dati o un driver, vedere [Scelta di un'origine dati o di un driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se le parole chiave vengono ripetute nella stringa di connessione, il driver utilizza il valore associato alla prima occorrenza della parola chiave. Se le parole chiave **DSN** e **DRIVER** sono incluse nella stessa stringa di connessione, Gestione Driver e il driver utilizzano la parola chiave corrispondente viene visualizzata per prima.  
  
 Le parole chiave **FILEDSN** e **DSN** si escludono a vicenda: viene utilizzata la parola chiave che appare per prima e quella che appare per seconda viene ignorata. Le parole chiave **FILEDSN** e **DRIVER,** d'altra parte, non si escludono a vicenda. Se una parola chiave viene visualizzata in una stringa di connessione con **FILEDSN**, viene utilizzato il valore dell'attributo della parola chiave nella stringa di connessione anziché il valore dell'attributo della stessa parola chiave nel file DSN.  
  
 Se viene utilizzata la parola chiave **FILEDSN,** le parole chiave specificate in un file DSN vengono utilizzate per creare una stringa di connessione. Per ulteriori informazioni, vedere "Origini dati file" più avanti in questa sezione. La parola chiave **UID** è facoltativa. un file .dsn può essere creato solo con la parola chiave **DRIVER.** La parola chiave **PWD** non viene memorizzata in un file DSN. La directory predefinita per il salvataggio e il caricamento di un file DSN sarà una combinazione del percorso specificato da **CommonFileDir** in HKEY_LOCAL_MACHINE SOFTWARE , Microsoft Windows CurrentVersion e "ODBC DataSources". (Se CommonFileDir fosse "C:"Programmi"File comuni", la directory predefinita sarà "C:.  
  
> [!NOTE]  
>  Un file DSN può essere modificato direttamente chiamando le funzioni [SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md) e [SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md) nella DLL del programma di installazione.  
  
 Se viene utilizzata la parola chiave **SAVEFILE,** i valori degli attributi delle parole chiave utilizzate per creare la connessione presente e corretta verranno salvati come file DSN con il nome del valore dell'attributo della parola chiave **SAVEFILE.** La parola chiave **SAVEFILE** deve essere utilizzata insieme alla parola chiave **DRIVER,** alla parola chiave **FILEDSN** o a entrambe oppure SQL_SUCCESS_WITH_INFO la funzione restituisce SQLSTATE 01S09 (parola chiave non valida). La parola chiave **SAVEFILE** deve essere presente prima della parola chiave **DRIVER** nella stringa di connessione, altrimenti i risultati non saranno definiti.  
  
## <a name="driver-manager-guidelines"></a>Linee guida per Gestione driver  
 Gestione Driver costruisce una stringa di connessione da passare al driver nel *InConnectionString* argomento del driver **SQLDriverConnect** funzione. Gestione Driver non modifica il *InConnectionString* argomento passato dall'applicazione.  
  
 L'azione di Gestione Driver si basa sul valore dell'argomento *DriverCompletion:*  
  
-   SQL_DRIVER_PROMPT: se la stringa di connessione non contiene la parola chiave **DRIVER**, **DSN**o **FILEDSN,** Gestione Driver visualizza la finestra di dialogo Origini dati . Costruisce una stringa di connessione dal nome dell'origine dati restituito dalla finestra di dialogo e da qualsiasi altra parola chiave passata dall'applicazione. Se il nome dell'origine dati restituito dalla finestra di dialogo è vuoto, Gestione Driver specifica la coppia parola chiave-valore DSN- Default. Questa finestra di dialogo non visualizza un'origine dati con il nome "Predefinito".  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: se la stringa di connessione specificata dall'applicazione include la parola chiave **DSN,** Gestione Driver copia la stringa di connessione specificata dall'applicazione. In caso contrario, vengono eseguite le stesse azioni eseguite quando *DriverCompletion* è SQL_DRIVER_PROMPT.  
  
-   SQL_DRIVER_NOPROMPT: Gestione Driver copia la stringa di connessione specificata dall'applicazione.  
  
 Se la stringa di connessione specificata dall'applicazione contiene la parola chiave **DRIVER,** Gestione Driver copia la stringa di connessione specificata dall'applicazione.  
  
 Utilizzando la stringa di connessione che ha costruito, Gestione Driver determina quale driver da utilizzare, si connette a tale driver e passa la stringa di connessione che ha costruito al driver; Per ulteriori informazioni sull'interazione di Gestione Driver e il driver, vedere la sezione "Commenti" in [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Se la stringa di connessione non contiene la parola chiave **DRIVER,** Gestione Driver determina quale driver da utilizzare come segue:  
  
1.  Se la stringa di connessione contiene la parola chiave **DSN,** Gestione Driver recupera il driver associato all'origine dati dalle informazioni di sistema.  
  
2.  Se la stringa di connessione non contiene la parola chiave **DSN** o l'origine dati non viene trovata, Gestione Driver recupera il driver associato all'origine dati predefinita dalle informazioni di sistema. Per ulteriori informazioni, vedere [Sottochiave predefinita.](../../../odbc/reference/install/default-subkey.md) Gestione Driver modifica il valore della parola chiave **DSN** nella stringa di connessione in "DEFAULT".  
  
3.  Se la parola chiave **DSN** nella stringa di connessione è impostata su "DEFAULT", Gestione Driver recupera il driver associato all'origine dati predefinita dalle informazioni di sistema.  
  
4.  Se l'origine dati non viene trovata e l'origine dati predefinita non viene trovata, Gestione Driver restituisce SQL_ERROR con SQLSTATE IM002 (origine dati non trovata e nessun driver predefinito specificato).  
  
## <a name="file-data-sources"></a>Origini dati di file  
 Se la stringa di connessione specificata dall'applicazione nella chiamata a **SQLDriverConnect** contiene la parola chiave **FILEDSN** e questa parola chiave non viene sostituita dalla parola chiave **DSN** o **DRIVER,** Gestione Driver crea una stringa di connessione utilizzando le informazioni nel file DSN e l'argomento *InConnectionString.* Gestione Driver procede come segue:  
  
1.  Controlla se il nome del file DSN è valido. In caso contrario, restituisce SQL_ERROR con SQLSTATE IM014 (nome non valido del DSN di file). Se il nome del file è una stringa vuota ("") e non è SQL_DRIVER_NOPROMPT specificato, viene visualizzata la finestra di dialogo **Apri file.** Se il nome del file contiene un percorso valido ma nessun nome file o nome di file non valido e SQL_DRIVER_NOPROMPT non è specificato, verrà visualizzata la finestra di dialogo **Apri file** con la directory corrente impostata su quella specificata nel nome file. Se il nome del file è una stringa vuota ("") o il nome del file contiene un percorso valido ma nessun nome di file o un nome di file non valido e viene specificato SQL_DRIVER_NOPROMPT, viene restituito SQL_ERROR con SQLSTATE IM014 (nome non valido del DSN di file).  
  
2.  Legge tutte le parole chiave nella sezione [ODBC] del file DSN. Se la parola chiave **DRIVER** non è presente, restituisce SQL_ERROR con SQLSTATE IM012 (errore di sintassi della parola chiave Driver), ad eccezione del caso in cui il file DSN non è condivisibile e pertanto contiene solo la parola chiave **DSN.**  
  
     Se l'origine dati file non è condissiva, Gestione Driver legge il valore della parola chiave **DSN** e si connette in base alle esigenze all'origine dati utente o di sistema a cui fa riferimento l'origine dati file non condivida. I passaggi da 3 a 5 non vengono eseguiti.  
  
3.  Costruisce una stringa di connessione per il driver. La stringa di connessione del driver è l'unione delle parole chiave specificate nel file DSN e quelle specificate nella stringa di connessione dell'applicazione originale. Regole per la costruzione della stringa di connessione del driver in cui le parole chiave si sovrappongono sono le seguenti:Rules for the construction of the driver connection string where keywords overlap are as follows:  
  
    -   Se la parola chiave **DRIVER** è presente nella stringa di connessione dell'applicazione e i driver specificati dalle parole chiave **DRIVER** non sono gli stessi nel file DSN e nella stringa di connessione dell'applicazione, le informazioni sul driver nel file DSN vengono ignorate e vengono utilizzate le informazioni sul driver nella stringa di connessione dell'applicazione. Se i driver specificati dalla parola chiave **DRIVER** sono gli stessi nel file DSN e nella stringa di connessione dell'applicazione, in cui tutte le parole chiave si sovrappongono, quelle specificate nella stringa di connessione dell'applicazione hanno la precedenza su quelle specificate nel file DSN.  
  
    -   Nella nuova stringa di connessione, la parola chiave **FILEDSN** viene eliminata.  
  
4.  Carica il driver esaminando la voce del Registro di sistema HKEY_LOCAL_MACHINE . INI\\<\>Driver Name \<(Nome driver) - Driver dove il nome del driver> è specificato dalla parola chiave **DRIVER.**  
  
5.  Passa il driver la nuova stringa di connessioni.  
  
 Per esempi di file DSN, vedere [Connessione tramite origini dati file](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md).  
  
## <a name="savefile-keyword"></a>SaveFILE (parola chiave)  
 Se la stringa di connessione specificata dall'applicazione contiene la parola chiave **SAVEFILE,** Gestione Driver salva la stringa di connessione in un file DSN. Gestione Driver procede come segue:  
  
1.  Controlla se il nome del file DSN incluso come valore dell'attributo della parola chiave **SAVEFILE** è valido. In caso contrario, restituisce SQL_ERROR con SQLSTATE IM014 (nome non valido del DSN di file). La validità del nome file è determinata dalle regole standard di denominazione del sistema. Se il nome del file è una stringa vuota ("") e il *DriverCompletion* argomento non è SQL_DRIVER_NOPROMPT, quindi il nome del file è valido. Se il nome del file esiste già, se *DriverCompletion* è SQL_DRIVER_NOPROMPT, il file viene sovrascritto. Se *DriverCompletion* è SQL_DRIVER_PROMPT, SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED, una finestra di dialogo richiede all'utente di specificare se il file deve essere sovrascritto. Se si immi non è stato immesso Alcun, viene visualizzata la finestra di dialogo **Salvataggio file.**  
  
2.  Se il driver restituisce SQL_SUCCESS e il nome del file non è una stringa vuota, quindi Gestione Driver scrive le informazioni di connessione restituite nel *OutConnectionString* argomento al file specificato con il formato specificato nella sezione "Stringhe di connessione" più indietro in questa sezione.  
  
3.  Se il driver restituisce SQL_SUCCESS e il nome del file è una stringa vuota (""), quindi Gestione Driver chiama la finestra di dialogo comune **di salvataggio File** con il *hwnd* specificato e scrive le informazioni di connessione restituite in *OutConnectionString* nel file specificato nella finestra di dialogo comune File-Save con il formato specificato nella sezione "Stringhe di connessione" più indietro in questa sezione.  
  
4.  Se il driver restituisce SQL_SUCCESS, restituisce il *OutConnectionString* argomento contenente la stringa di connessione all'applicazione.  
  
5.  Se il driver restituisce SQL_SUCCESS_WITH_INFO o SQL_ERROR, Gestione Driver restituisce il SQLSTATE all'applicazione.  
  
## <a name="driver-guidelines"></a>Linee guida per i driver  
 Il driver controlla se la stringa di connessione passata da Gestione Driver contiene la parola chiave **DSN** o **DRIVER.** Se la stringa di connessione contiene la parola chiave **DRIVER,** il driver non può recuperare informazioni sull'origine dati dalle informazioni di sistema. Se la stringa di connessione contiene la parola chiave **DSN** o non contiene il **DSN** o la parola chiave **DRIVER,** il driver può recuperare informazioni sull'origine dati dalle informazioni di sistema come segue:  
  
1.  Se la stringa di connessione contiene la parola chiave **DSN,** il driver recupera le informazioni per l'origine dati specificata.  
  
2.  Se la stringa di connessione non contiene la parola chiave **DSN,** l'origine dati specificata non viene trovata o la parola chiave **DSN** è impostata su "DEFAULT", il driver recupera le informazioni per l'origine dati predefinita.  
  
 Il driver utilizza tutte le informazioni che recupera dalle informazioni di sistema per aumentare le informazioni passate nella stringa di connessione. Se le informazioni nelle informazioni di sistema duplicano le informazioni nella stringa di connessione, il driver utilizza le informazioni nella stringa di connessione.  
  
 In base al valore di *DriverCompletion*, il driver richiede all'utente le informazioni di connessione, ad esempio l'ID utente e la password, e si connette all'origine dati:  
  
-   SQL_DRIVER_PROMPT: il driver visualizza una finestra di dialogo, utilizzando i valori della stringa di connessione e le informazioni di sistema (se presenti) come valori iniziali. Quando l'utente esce dalla finestra di dialogo, il driver si connette all'origine dati. Costruisce inoltre una stringa di connessione dal valore **DRIVER** della parola \*chiave **DSN** o DRIVER in *InConnectionString* e dalle informazioni restituite dalla finestra di dialogo. Questa stringa di connessione viene insediata nel buffer*di OutConnectionString.*  
  
-   SQL_DRIVER_COMPLETE o SQL_DRIVER_COMPLETE_REQUIRED: se la stringa di connessione contiene informazioni sufficienti e tali informazioni \*sono corrette, il driver si connette all'origine dati e copia *InConnectionString* in \* *OutConnectionString*. Se le informazioni sono mancanti o errate, il driver esegue le stesse azioni eseguite quando *DriverCompletion* è SQL_DRIVER_PROMPT, ad eccezione del fatto che se *DriverCompletion* è SQL_DRIVER_COMPLETE_REQUIRED, il driver disabilita i controlli per tutte le informazioni non necessarie per connettersi all'origine dati.  
  
-   SQL_DRIVER_NOPROMPT: se la stringa di connessione contiene informazioni sufficienti, \*il driver \*si connette all'origine dati e copia *InConnectionString* in *OutConnectionString*. In caso contrario, il driver restituisce SQL_ERROR per **SQLDriverConnect**.  
  
 In caso di connessione corretta all'origine dati, il driver imposta \*anche *StringLength2Ptr* sulla lunghezza della stringa di connessione di output che è disponibile per la restituzione in*OutConnectionString*.  
  
 Se l'utente annulla una finestra di dialogo visualizzata da Gestione Driver o dal driver, **SQLDriverConnect** restituisce SQL_NO_DATA.  
  
 Per informazioni sull'interazione tra Gestione driver e il driver durante il processo di connessione, vedere [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Se un driver supporta **SQLDriverConnect**, la sezione della parola chiave del driver per il driver deve contenere la parola chiave **ConnectFunctions** con il secondo set di caratteri "Y".  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>Connessione quando il pool di connessioni è abilitatoConnecting When Connection Pooling is Enabled  
 Il pool di connessioni consente a un'applicazione di riutilizzare una connessione già creata. Quando **SQLDriverConnect** viene chiamato, Gestione Driver tenta di effettuare la connessione utilizzando una connessione che fa parte di un pool di connessioni in un ambiente che è stato designato per il pool di connessioni. Per ulteriori informazioni sul pool di connessioni, vedere [Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md).  
  
 Un'applicazione può impostare SQL_ATTR_RESET_CONNECTION prima di chiamare SQLDisconnect su una connessione in cui è abilitato il pooling. Per ulteriori informazioni, vedere [Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Le restrizioni seguenti si applicano quando un'applicazione chiama SQLDriverConnect per connettersi a una connessione in pool:The following restrictions apply when an application calls **SQLDriverConnect** to connect to a pooled connection:  
  
-   Nessuna elaborazione del pool di connessioni viene eseguita quando la parola chiave **SAVEFILE** è specificata nella stringa di connessione.  
  
-   Se il pool di connessioni è abilitato, **SQLDriverConnect** può essere chiamato solo con un *DriverCompletion* argomento di SQL_DRIVER_NOPROMPT; se **SQLDriverConnect** viene chiamato con qualsiasi altro *DriverCompletion*, SQLSTATE HY110 (completamento del driver non valido) verrà restituito.  
  
## <a name="connection-attributes"></a>Attributi di connessione  
 Il SQL_ATTR_LOGIN_TIMEOUTattributo di connessione, impostato tramite **SQLSetConnectAttr**, definisce il numero di secondi di attesa per il completamento di una richiesta di accesso con una connessione corretta da parte del driver prima di tornare all'applicazione. Se all'utente viene richiesto di completare la stringa di connessione, un periodo di attesa per ogni richiesta di accesso inizia quando il driver avvia il processo di connessione.  
  
 Il driver apre la connessione in modalità di accesso SQL_MODE_READ_WRITE per impostazione predefinita. Per impostare la modalità di accesso su SQL_MODE_READ_ONLY, l'applicazione deve chiamare **SQLSetConnectAttr** con l'attributo SQL_ATTR_ACCESS_MODE prima di chiamare **SQLDriverConnect**.  
  
 Se nelle informazioni di sistema per l'origine dati viene specificata una libreria di traduzione predefinita, il driver la carica. È possibile caricare una libreria di traduzione diversa chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_LIB. Un'opzione di conversione può essere specificata chiamando **SQLSetConnectAttr** con l'opzione SQL_ATTR_TRANSLATE_OPTION.  
  
 Per ulteriori informazioni, vedere [Connessione con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md).  
  
```cpp  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
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
  
 Vedere anche [Programma ODBC di esempio](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Individuazione ed enumerazione dei valori necessari per connettersi a un'origine datiDiscovering and enumerating values required to connect to a data source|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnectSQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Disconnessione da un'origine datiDisconnecting from a data source|[Funzione SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|Restituzione delle descrizioni e degli attributi dei driver|[Funzione SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|Liberare una maniglia|[SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
