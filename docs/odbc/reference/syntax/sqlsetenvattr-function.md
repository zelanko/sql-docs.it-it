---
title: SqlSetEnvAttr (funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299541"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr Function
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLSetEnvAttr** imposta gli attributi che regolano gli aspetti degli ambienti.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Ingresso] Maniglia dell'ambiente.  
  
 *Attributo*  
 [Ingresso] Attributo da impostare, elencato in "Commenti".  
  
 *ValuePtr*  
 [Ingresso] Puntatore al valore da associare *all'attributo*. A seconda del valore di *Attribute*, *ValuePtr* sarà un valore integer a 32 bit o punterà a una stringa di caratteri con terminazione null.  
  
 *Lunghezza stringa*  
 [Ingresso] Se *ValuePtr* fa riferimento a una stringa di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di*ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *ValuePtr* è un numero intero, *StringLength* viene ignorato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetEnvAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_ENV e un *handle* di *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLSetEnvAttr** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente. Se un driver non supporta un attributo di ambiente, l'errore può essere restituito solo durante la connessione.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01S02 (in questo stato di|Valore dell'opzione modificato|Il driver non supportava il valore specificato in *ValuePtr* e ha sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|I009|Utilizzo non valido del puntatore null|L'argomento Attribute ha identificato un attributo di ambiente che richiedeva un valore stringa e l'argomento *ValuePtr* era un puntatore null.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) Un handle di connessione è stato allocato in *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** non è stata impostata con **SQLSetEnvAttr** e *attributo* non è uguale a **SQL_ATTR_ODBC_VERSION**. Non è necessario impostare **SQL_ATTR_ODBC_VERSION** in modo esplicito se si utilizza **SQLAllocHandleStd**.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY024 (informazioni in base al|Valore dell'attributo non valido|Dato il valore *Attribute* specificato, è stato specificato un valore non valido in *ValuePtr*.|  
|I090|Stringa o lunghezza del buffer non valida|L'argomento *StringLength* è minore di 0 ma non è SQL_NTS.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|(DM) il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportata dal driver.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il valore specificato per l'argomento *attributo* è un attributo di ambiente ODBC valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver.<br /><br /> (DM) l'argomento *Attribute* è stato SQL_ATTR_OUTPUT_NTS e *ValuePtr* è stato SQL_FALSE.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLSetEnvAttr** solo se nell'ambiente non è allocato alcun handle di connessione. Tutti gli attributi di ambiente impostati correttamente dall'applicazione per l'ambiente persistono fino a quando **SQLFreeHandle** viene chiamato sull'ambiente. In ODBC *3.x*è possibile allocare contemporaneamente più handle di ambiente.  
  
 Il formato delle informazioni impostate tramite *ValuePtr* dipende *dall'attributo*specificato. **SQLSetEnvAttr** accetterà le informazioni sugli attributi in uno dei due formati diversi: una stringa di caratteri con terminazione null o un valore integer a 32 bit. Il formato di ciascuno è indicato nella descrizione dell'attributo.  
  
 Non sono presenti attributi di ambiente specifici del driver.  
  
 Gli attributi di connessione non possono essere impostati da una chiamata a **SQLSetEnvAttr**. Se si tenta di eseguire questa operazione, verrà restituito SQLSTATE HY092 (identificatore di attributo/opzione non valido).  
  
|*Attributo*|*Contenuto ValuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Valore SQLUINTEGER a 32 bit che abilita o disabilita il pool di connessioni a livello di ambiente. Vengono utilizzati i seguenti valori:<br /><br /> SQL_CP_OFF: il pool di connessioni è disattivato. Questa è la modalità predefinita.<br /><br /> SQL_CP_ONE_PER_DRIVER: per ogni driver è supportato un singolo pool di connessioni. Ogni connessione in un pool è associata a un driver.<br /><br /> SQL_CP_ONE_PER_HENV: è supportato un singolo pool di connessioni per ogni ambiente. Ogni connessione in un pool è associata a un ambiente.<br /><br /> SQL_CP_DRIVER_AWARE: utilizzare la funzionalità di riconoscimento del pool di connessioni del driver, se disponibile. Se il driver non supporta il riconoscimento del pool di connessioni, SQL_CP_DRIVER_AWARE viene ignorato e viene utilizzato SQL_CP_ONE_PER_HENV. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver . In un ambiente in cui alcuni driver supportano e alcuni driver non supportano il riconoscimento del pool di connessioni, SQL_CP_DRIVER_AWARE possibile abilitare la funzionalità di riconoscimento del pool di connessioni su quelli che supportano i driver, ma equivale a SQL_CP_ONE_PER_HENV su quei driver che non supportano la funzionalità di riconoscimento del pool di connessioni.<br /><br /> Il pool di connessioni viene abilitato chiamando **SQLSetEnvAttr** per impostare l'attributo SQL_ATTR_CONNECTION_POOLING su SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Questa chiamata deve essere effettuata prima che l'applicazione allochi l'ambiente condiviso per il quale deve essere abilitato il pool di connessioni. L'handle di ambiente nella chiamata a **SQLSetEnvAttr** è impostato su null, che rende SQL_ATTR_CONNECTION_POOLING un attributo a livello di processo. Dopo aver abilitato il pool di connessioni, l'applicazione alloca un ambiente condiviso implicito chiamando **SQLAllocHandle** con il *InputHandle* argomento impostato su SQL_HANDLE_ENV.<br /><br /> Dopo che il pool di connessioni è stato abilitato ed è stato selezionato un ambiente condiviso per un'applicazione, SQL_ATTR_CONNECTION_POOLING non può essere reimpostato per tale ambiente, perché **SQLSetEnvAttr** viene chiamato con un handle di ambiente null durante l'impostazione di questo attributo. Se questo attributo è impostato mentre il pool di connessioni è già abilitato in un ambiente condiviso, l'attributo influisce solo sugli ambienti condivisi allocati successivamente.<br /><br /> È anche possibile abilitare il pool di connessioni in un ambiente. Tenere presente quanto segue sul pool di connessioni dell'ambiente:Note the following about environment connection pooling:<br /><br /> - L'abilitazione del pool di connessioni su un handle NULL è un attributo a livello di processo.- Enabling connection pooling on a NULL handle is a process-level attribute. Gli ambienti allocati successivamente saranno un ambiente condiviso ed erediteranno l'impostazione del pool di connessioni a livello di processo.<br />- Dopo l'allocazione di un ambiente, un'applicazione può comunque modificare l'impostazione del pool di connessioni.<br />- Se il pool di connessioni dell'ambiente è abilitato e il driver della connessione utilizza il pool di driver, il pool ingaggio dell'ambiente ha la preferenza.<br /><br /> SQL_ATTR_CONNECTION_POOLING viene implementata all'interno di Gestione Driver. Non è necessario che un driver implementi SQL_ATTR_CONNECTION_POOLING. Le applicazioni ODBC 2.0 e 3.0 possono impostare questo attributo di ambiente.<br /><br /> Per altre informazioni, vedere la pagina relativa ai [pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Valore SQLUINTEGER a 32 bit che determina la modalità di scelta di una connessione da un pool di connessioni. Quando **SQLConnect** o **SQLDriverConnect** viene chiamato, Gestione Driver determina quale connessione viene riutilizzata dal pool. Gestione Driver tenta di far corrispondere le opzioni di connessione nella chiamata e gli attributi di connessione impostati dall'applicazione per le parole chiave e gli attributi di connessione delle connessioni nel pool. Il valore di questo attributo determina il livello di precisione dei criteri di corrispondenza.<br /><br /> I seguenti valori vengono utilizzati per impostare il valore di questo attributo:<br /><br /> SQL_CP_STRICT_MATCH: vengono riutilizzate solo le connessioni che corrispondono esattamente alle opzioni di connessione nella chiamata e gli attributi di connessione impostati dall'applicazione. Questa è la modalità predefinita.<br /><br /> SQL_CP_RELAXED_MATCH: è possibile utilizzare connessioni con parole chiave corrispondenti della stringa di connessione. Le parole chiave devono corrispondere, ma non tutti gli attributi di connessione devono corrispondere.<br /><br /> Per ulteriori informazioni su come Gestione Driver esegue la corrispondenza nella connessione a una connessione in pool, vedere [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Per ulteriori informazioni sul pool di connessioni, vedere [Pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Intero a 32 bit che determina se determinate funzionalità presentano il comportamento ODBC *2.x* o ODBC *3.x.* I seguenti valori vengono utilizzati per impostare il valore di questo attributo:<br /><br /> SQL_OV_ODBC3_80 : Gestione driver e il driver presentano il seguente comportamento ODBC 3.8:<br /><br /> - Il driver restituisce e prevede codici ODBC *3.x* per data, ora e timestamp.<br />- Il driver restituisce codici SQLSTATE ODBC *3.x* quando vengono chiamati **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- L'argomento CatalogName in una chiamata a SQLTables accetta un criterio di ricerca.- The *CatalogName* argument in a call to **SQLTables** accepts a search pattern.<br />- Gestione Driver supporta l'estendibilità del tipo di dati C.- The Driver Manager supports C data type extensibility. Per ulteriori informazioni sull'estensibilità dei tipi di dati C, vedere [Tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Per ulteriori informazioni, vedere Novità di [ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3: Gestione driver e il driver presentano il seguente comportamento ODBC *3.x:*<br /><br /> - Il driver restituisce e prevede codici ODBC *3.x* per data, ora e timestamp.<br />- Il driver restituisce codici SQLSTATE ODBC *3.x* quando vengono chiamati **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- L'argomento CatalogName in una chiamata a SQLTables accetta un criterio di ricerca.- The *CatalogName* argument in a call to **SQLTables** accepts a search pattern.<br />- Gestione Driver non supporta l'estendibilità del tipo di dati C.- The Driver Manager does not support C data type extensibility.<br /><br /> SQL_OV_ODBC2: Gestione driver e il driver presentano il seguente comportamento ODBC *2.x.* Ciò è particolarmente utile per un'applicazione ODBC *2.x* che utilizza un driver ODBC *3.x.*<br /><br /> - Il driver restituisce e prevede codici ODBC *2.x* per data, ora e timestamp.<br />- Il driver restituisce codici SQLSTATE ODBC *2.x* quando vengono chiamati **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- L'argomento CatalogName in una chiamata a SQLTables non accetta un criterio di ricerca.- The *CatalogName* argument in a call to **SQLTables** does not accept a search pattern.<br />- Gestione Driver non supporta l'estendibilità del tipo di dati C.- The Driver Manager does not support C data type extensibility.<br /><br /> Un'applicazione deve impostare questo attributo di ambiente prima di chiamare qualsiasi funzione che dispone di un SQLHENV argomento o la chiamata restituirà SQLSTATE HY010 (errore di sequenza di funzione). È specifico del driver se esiste un comportamento aggiuntivo per questi flag ambientali.<br /><br /> Per ulteriori informazioni, vedere Dichiarazione della [versione ODBC dell'applicazione](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [delle modifiche comportamentali](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Intero a 32 bit che determina il modo in cui il driver restituisce i dati stringa. Se SQL_TRUE, il driver restituisce i dati stringa con terminazione null. Se SQL_FALSE, il driver non restituisce dati di stringa con terminazione null.<br /><br /> Il valore predefinito di questo attributo è SQL_TRUE. Una chiamata a **SQLSetEnvAttr** per impostarlo su SQL_TRUE restituisce SQL_SUCCESS. Una chiamata a **SQLSetEnvAttr** per impostarla su SQL_FALSE restituisce SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata).|  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di una maniglia|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Restituzione dell'impostazione di un attributo di ambienteReturning the setting of an environment attribute|[Funzione SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
