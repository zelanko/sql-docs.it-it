---
title: Funzione SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61b83ee255e580c557bfae9923d67735c63c3912
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202158"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr Function
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLSetEnvAttr** imposta gli attributi che determinano gli aspetti degli ambienti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Input] Handle di ambiente.  
  
 *Attribute*  
 [Input] Attributo da impostare, elencato in "Commenti".  
  
 *ValuePtr*  
 [Input] Puntatore al valore da associare *attributo*. A seconda del valore di *attributo*, *ValuePtr* verranno un valore integer a 32 bit o puntare a una stringa di caratteri con terminazione null.  
  
 *StringLength*  
 [Input] Se *ValuePtr* punta a una stringa di caratteri o binario buffer, questo argomento deve essere la lunghezza di **ValuePtr*. Per i dati di stringa di caratteri, questo argomento deve contenere il numero di byte nella stringa.  
  
 Se *ValuePtr* è un intero *StringLength* viene ignorato.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetEnvAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_ENV e un *gestiscono* dei *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLSetEnvAttr** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente. Se un driver non supporta un attributo di ambiente, l'errore può essere restituito solo durante la fase di connessione.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore di opzione modificato|Il driver non supportava il valore specificato nel *ValuePtr* e sostituito un valore simile. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY009|Utilizzo non valido del puntatore null|L'argomento dell'attributo identificato un attributo di ambiente che un valore di stringa, obbligatorio e il *ValuePtr* argomento era un puntatore null.|  
|HY010|Errore nella sequenza della funzione|(DM) è stato allocato un handle di connessione sul *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** non è stata impostata con **SQLSetEnvAttr** e *attributo* non è uguale a **SQL_ATTR_ODBC_VERSION**. Non è necessario impostare **SQL_ATTR_ODBC_VERSION** in modo esplicito se si usa **SQLAllocHandleStd**.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY024|Valore dell'attributo non valido|Dato l'oggetto specificato *attributo* valore, in cui è stato specificato un valore non valido *ValuePtr*.|  
|HY090|Lunghezza della stringa o buffer non valido|Il *StringLength* argomento era minore di 0 ma non era SQL_NTS.|  
|HY092|Identificatore di attributo/opzione non è valido|(DM) il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportati dal driver.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Il valore specificato per l'argomento *attributo* era un attributo di ambiente ODBC valido per la versione di ODBC supportati dal driver, ma non era supportata dal driver.<br /><br /> (DM) di *attributo* argomento era SQL_ATTR_OUTPUT_NTS, e *ValuePtr* era SQL_FALSE.|  
  
## <a name="comments"></a>Commenti  
 Un'applicazione può chiamare **SQLSetEnvAttr** solo se non esistono handle di connessione è stato allocato nell'ambiente. Tutti gli attributi di ambiente è stati impostati dall'applicazione per l'ambiente vengono mantenute fino **SQLFreeHandle** viene chiamato nell'ambiente. Più di un handle di ambiente può essere allocato contemporaneamente in ODBC 3*x*.  
  
 Imposta il formato delle informazioni attraverso *ValuePtr* dipende specificato *attributo*. **SQLSetEnvAttr** accetterà le informazioni sugli attributi in uno dei due formati: stringa di caratteri con terminazione null o un valore integer a 32 bit. Il formato della ognuno viene indicato nella descrizione dell'attributo.  
  
 Non sono presenti attributi di ambiente specifiche del driver.  
  
 Impossibile impostare gli attributi di connessione da una chiamata a **SQLSetEnvAttr**. Il tentativo di eseguire questa operazione restituisce SQLSTATE HY092 (identificatore di attributo/opzione non valida).  
  
|*Attribute*|*ValuePtr* contenuto|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Valore SQLUINTEGER 32 bit che abilita o disabilita il pool di connessioni a livello di ambiente. Vengono usati i valori seguenti:<br /><br /> SQL_CP_OFF = Connection pooling è disattivato. Impostazione predefinita.<br /><br /> SQL_CP_ONE_PER_DRIVER = un singolo pool di connessioni è supportato per ogni driver. Ogni connessione in un pool è associata a un driver.<br /><br /> SQL_CP_ONE_PER_HENV = un singolo pool di connessioni è supportato per ogni ambiente. Ogni connessione in un pool è associata a un ambiente.<br /><br /> SQL_CP_DRIVER_AWARE = Usa la funzionalità di riconoscimento dei pool di connessioni del driver, se disponibile. Se il driver non supporta la consapevolezza di pool di connessioni, SQL_CP_DRIVER_AWARE viene ignorato e viene usato SQL_CP_ONE_PER_HENV. Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). In un ambiente in cui alcuni driver supportano e alcuni driver non supportano il riconoscimento dei pool di connessioni, SQL_CP_DRIVER_AWARE può abilitare la funzionalità di riconoscimento dei pool di connessioni in quelli che supportano il driver, ma è equivalente all'impostazione di SQL_CP_ONE_PER_HENV su i driver che non supportano la funzionalità di riconoscimento dei pool di connessioni.<br /><br /> Pool di connessioni è abilitato chiamando **SQLSetEnvAttr** su cui impostare l'attributo SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Prima che l'applicazione viene allocata per la connessione che il pool è necessario abilitare ambiente condiviso, è necessario effettuare questa chiamata. L'handle di ambiente nella chiamata a **SQLSetEnvAttr** è impostato su null, il che rende SQL_ATTR_CONNECTION_POOLING un attributo a livello di processo. Dopo aver abilitato la limitazione delle richieste di connessione, quindi l'applicazione esegue l'allocazione di un ambiente condiviso implicito chiamando **SQLAllocHandle** con il *InputHandle* argomento impostato su SQL_HANDLE_ENV.<br /><br /> Dopo che il pool di connessioni è stato abilitato e un ambiente condiviso è stato selezionato per un'applicazione, è possibile reimpostare SQL_ATTR_CONNECTION_POOLING per quell'ambiente, perché **SQLSetEnvAttr** viene chiamato con un ambiente null gestire quando si imposta questo attributo. Se questo attributo viene impostato anche se il pool di connessioni è già abilitato in un ambiente condiviso, l'attributo interessa solo gli ambienti condivisi allocati successivamente.<br /><br /> È anche possibile abilitare il pool di connessioni in un ambiente. Tenere presente quanto segue sui pool di connessioni di ambiente:<br /><br /> -Abilitazione del pool di connessioni su un handle NULL è un attributo a livello di processo. Gli ambienti successivamente allocati saranno un ambiente condiviso ed erediteranno il pool di impostazione di connessioni a livello di processo.<br />-Dopo che è stato allocato un ambiente, un'applicazione può comunque in grado di modificare l'impostazione del pool di connessione.<br />-Se ambiente pool di connessioni è abilitato e driver della connessione viene utilizzato un pool di driver, il pool di ambiente ha la preferenza.<br /><br /> SQL_ATTR_CONNECTION_POOLING viene implementato all'interno di gestione Driver. Un driver non è necessario implementare SQL_ATTR_CONNECTION_POOLING. ODBC 2.0 e 3.0 applicazioni possono impostare l'attributo di ambiente.<br /><br /> Per altre informazioni, vedere la pagina relativa ai [pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Valore SQLUINTEGER 32 bit che determina la modalità di scelta di una connessione da un pool di connessioni. Quando **SQLConnect** oppure **SQLDriverConnect** viene chiamato, gestione Driver determina la connessione viene riutilizzata dal pool. Gestione Driver Cerca la corrispondenza con le opzioni di connessione della chiamata e gli attributi di connessione impostati dall'applicazione per le parole chiave e gli attributi di connessione delle connessioni nel pool. Il valore di questo attributo determina il livello di precisione dei criteri di corrispondenza.<br /><br /> Per impostare il valore di questo attributo vengono usati i valori seguenti:<br /><br /> SQL_CP_STRICT_MATCH = solo le connessioni che corrispondono esattamente le opzioni di connessione nella chiamata e la connessione vengono riutilizzati attributi impostati dall'applicazione. Impostazione predefinita.<br /><br /> SQL_CP_RELAXED_MATCH = connessioni con stringa di connessione da utilizzare le parole chiave corrispondenti. Devono corrispondere a parole chiave, ma non tutti gli attributi di connessione devono corrispondere.<br /><br /> Per altre informazioni sul modo in cui viene eseguita la corrispondenza per la connessione a una connessione in pool gestione Driver, vedere [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Per altre informazioni sui pool di connessioni, vedere [pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Un valore integer a 32 bit che determina se determinate funzionalità presenta ODBC 2 *. x* comportamento o ODBC 3*x* comportamento. Per impostare il valore di questo attributo vengono usati i valori seguenti:<br /><br /> SQL_OV_ODBC3_80 = The Driver Manager e il comportamento di driver di ODBC 3.8. seguente documento:<br /><br /> -Il driver restituisce e prevede che ODBC 3. *x* codici per date, time e timestamp.<br />-Il driver restituisce ODBC 3. *x* quando i codici SQLSTATE **SQLError**, **SQLGetDiagField**, oppure **SQLGetDiagRec** viene chiamato.<br />-il *CatalogName* argomento nella chiamata a **SQLTables** accetta un criterio di ricerca.<br />-Gestione Driver supporta l'estendibilità del tipo di dati C. Per altre informazioni sull'estendibilità del tipo di dati C, vedere [tipi di dati C in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Per altre informazioni, vedere [What ' s New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = The Driver Manager e il documento di driver ODBC 3 seguente*x* comportamento:<br /><br /> -Il driver restituisce e si aspetta che ODBC 3*x* codici per date, time e timestamp.<br />-Il driver restituisce ODBC 3 *. x* quando i codici SQLSTATE **SQLError**, **SQLGetDiagField**, oppure **SQLGetDiagRec** viene chiamato.<br />-il *CatalogName* argomento nella chiamata a **SQLTables** accetta un criterio di ricerca.<br />-Gestione Driver non supporta l'estendibilità del tipo di dati C.<br /><br /> SQL_OV_ODBC2 = The Driver Manager e il documento di driver ODBC 2 seguente*x* comportamento. Ciò è particolarmente utile per un'API ODBC 2 *. x* funziona con un'applicazione ODBC 3*x* driver.<br /><br /> -Il driver restituisce e prevede 2 ODBC*x* codici per date, time e timestamp.<br />-Il driver restituisce 2 ODBC *. x* quando i codici SQLSTATE **SQLError**, **SQLGetDiagField**, oppure **SQLGetDiagRec** viene chiamato.<br />-il *CatalogName* argomento nella chiamata a **SQLTables** non accetta un criterio di ricerca.<br />-Gestione Driver non supporta l'estendibilità del tipo di dati C.<br /><br /> Un'applicazione deve impostare questo attributo di ambiente prima di chiamare qualsiasi funzione che dispone di un argomento SQLHENV o la chiamata restituisce SQLSTATE HY010 (funzione di errore nella sequenza). È specifico del driver eventuale comportamenti aggiuntivi per questi flag ambientali.<br /><br /> -Per altre informazioni, vedere [dichiarazione della versione dell'applicazione ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Valore intero a 32 bit che determina come il driver restituisce dati di tipo stringa. Se SQL_TRUE, il driver restituisce dati di tipo stringa con terminazione null. Se SQL_FALSE, il driver non restituisce dati di tipo stringa con terminata null.<br /><br /> Questo attributo viene impostato su SQL_TRUE. Una chiamata a **SQLSetEnvAttr** per impostarlo su SQL_TRUE restituisce SQL_SUCCESS. Una chiamata a **SQLSetEnvAttr** per impostarlo su restituisce SQL_FALSE SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata).|  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Allocazione di un handle|[Funzione SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Restituisce l'impostazione di un attributo di ambiente|[Funzione SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novità di ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
