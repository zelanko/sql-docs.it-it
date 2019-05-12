---
title: Funzione SQLMoreResults | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd3569425a862efd662c894c6839eb6df0f767e
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536512"
---
# <a name="sqlmoreresults-function"></a>Funzione SQLMoreResults
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLMoreResults** determina se sono disponibili in un'istruzione che contiene i risultati di ulteriori **selezionate**, **UPDATE**, **Inserisci**, o  **Elimina** istruzioni e, in caso affermativo, inizializza l'elaborazione per la restituzione dei risultati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>Argomenti  
 *StatementHandle*  
 [Input] Handle di istruzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_NO_DATA, SQL_ERROR, SQL_INVALID_HANDLE, OR SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLMoreResults** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _HANDLE_STMT e un *gestiscono* dei *StatementHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLMoreResults** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01S02|Valore dell'opzione è stato modificato|Il valore di un attributo di istruzione modificato come il batch è stato elaborato. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|08S01|Errore del collegamento di comunicazione|Il collegamento di comunicazione tra il driver e l'origine dati a cui è stato connesso il driver non è stato possibile prima dell'elaborazione di funzione è stata completata.|  
|40001|Errore di serializzazione.|Il rollback della transazione a causa di un deadlock delle risorse con un'altra transazione.|  
|40003|Completamento dell'istruzione sconosciuto|La connessione associata non è riuscita durante l'esecuzione di questa funzione e non è possibile determinare lo stato della transazione.|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY008|Operazione annullata|L'elaborazione asincrona è stata abilitata per il *StatementHandle*. Il **SQLMoreResults** funzione è stata chiamata e, prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** veniva chiamato sul *StatementHandle* . L'oggetto **SQLMoreResults** funzione è stata chiamata nuovamente sulle *StatementHandle*.<br /><br /> Il **SQLMoreResults** funzione è stata chiamata e, prima esecuzione, completata **SQLCancel** o **SQLCancelHandle** veniva chiamato sul *StatementHandle*  da un thread diverso in un'applicazione multithread.|  
|HY010|Errore nella sequenza della funzione|(DM) a cui è stata chiamata per l'handle di connessione che è associata una funzione in modo asincrono in esecuzione la *StatementHandle*. Questa funzione asincrona era ancora in esecuzione quando il **SQLMoreResults** funzione è stata chiamata.<br /><br /> (DM) a cui è stata chiamata per una funzione in modo asincrono in esecuzione, non è presente uno, il *StatementHandle* ed era ancora in esecuzione quando è stata chiamata questa funzione.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, oppure **SQLSetPos** è stato chiamato per il  *StatementHandle* e restituito SQL_NEED_DATA. Questa funzione è stata chiamata prima dei dati è stati inviati per tutti i parametri data-at-execution o più colonne.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Timeout di connessione scaduto|Il periodo di timeout di connessione è scaduto prima che l'origine dati ha risposto alla richiesta. Il periodo di timeout di connessione viene impostato tramite **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver non supporta questa funzione|Il driver (DM) associato il *StatementHandle* non supporta la funzione.|  
|IM017|Polling è disabilitato in modalità di notifica asincrona|Ogni volta che viene usato il modello di notifica, viene disabilitato il polling.|  
|IM018|**SQLCompleteAsync** non è stato chiamato per completare l'operazione asincrona precedente in questo handle.|Se la chiamata di funzione precedente dell'handle di restituisce SQL_STILL_EXECUTING e se è abilitata la modalità di notifica, **SQLCompleteAsync** deve essere chiamato su handle per eseguire operazioni di post-elaborazione e completare l'operazione.|  
  
## <a name="comments"></a>Commenti  
 **Selezionare** istruzioni restituiscono set di risultati. **UPDATE**, **inserire**, e **eliminare** istruzioni restituiscono un conteggio delle righe interessate. Se uno qualsiasi di queste istruzioni vengono eseguite in batch, inviato con le matrici di parametri (numerati in ordine di parametro, nell'ordine in cui appaiono nel batch crescente) o nelle procedure possono restituire più set di risultati o conteggio delle righe. Per informazioni su batch di istruzioni e le matrici di parametri, vedere [batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) e [matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Dopo l'esecuzione del batch, l'applicazione viene posizionata sul primo set di risultati. L'applicazione può chiamare **SQLBindCol**, **SQLBulkOperations**, **SQLFetch**, **SQLGetData**, **SQLFetchScroll** , **SQLSetPos**e tutte le funzioni dei metadati, nel set di risultati prima o successiva, esattamente come verrebbe restituito se si sono verificati solo un singolo set di risultati. Al termine con il primo set di risultati, l'applicazione chiama **SQLMoreResults** per passare al set di risultati successivo. Se è disponibile, un altro set di risultati o conteggio **SQLMoreResults** restituisce SQL_SUCCESS e ne inizializza il set di risultati o conteggio per un'ulteriore elaborazione. Se tutte le istruzioni di generazione di conteggio delle righe viene visualizzato tra causare che generano set di istruzioni, può essere rientri failover chiamando **SQLMoreResults**. Dopo la chiamata **SQLMoreResults** per **UPDATE**, **Inserisci**, oppure **Elimina** (istruzioni), un'applicazione può chiamare **SQLRowCount**.  
  
 Se si è verificato un correnti set di risultati con le righe non recuperate **SQLMoreResults** ignora tale set di risultati e rende il successivo set di risultati o conteggio disponibili. Se tutti i risultati sono stati elaborati, **SQLMoreResults** restituisce SQL_NO_DATA. Per alcuni driver, i parametri di output e valori restituiti non sono disponibili fino a quando non sono stati elaborati tutti i set di risultati e i conteggi delle righe. Per tale driver, i parametri di output e restituire valori diventi disponibili quando **SQLMoreResults** restituisce SQL_NO_DATA.  
  
 Tutti i binding sono stati stabiliti il precedenti set di risultati ancora restano validi. Se le strutture di colonna sono diverse per questo set di risultati, quindi chiamare **SQLFetch** oppure **SQLFetchScroll** può comportare un errore o troncamento. Per evitare questo problema, l'applicazione deve chiamare **SQLBindCol** in modo esplicito la riassociazione come appropriato (o tale scopo, impostare i campi di descrizione). In alternativa, l'applicazione può chiamare **SQLFreeStmt** con un *opzione* su SQL_UNBIND per annullare l'associazione di tutti i buffer di colonna.  
  
 I valori degli attributi di istruzione, ad esempio tipo di cursore, concorrenza dei cursori, dimensione del keyset o la lunghezza massima possono cambiare mentre l'applicazione passa attraverso il batch tramite chiamate a **SQLMoreResults**. In questo caso **SQLMoreResults** restituirà SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valore dell'opzione modificata).  
  
 La chiamata **SQLCloseCursor**, o **SQLFreeStmt** con un *opzione* di SQL_CLOSE, Elimina tutti i set di risultati e i conteggi delle righe che non erano disponibili come risultato l'esecuzione di il batch. L'handle di istruzione restituisce lo stato allocato o preparato. La chiamata **SQLCancel** per annullare una funzione in modo asincrono in esecuzione quando un batch è stato eseguito e l'handle di istruzione nel eseguito, cursore posizionato, o lo stato asincrono comporta set di tutti i risultati e i conteggi delle righe generato da batch viene ignorato se la chiamata di annullamento ha avuto esito positivo. L'istruzione restituisce quindi allo stato preparato o allocato.  
  
 Se altre istruzioni SQL con una combinazione di un batch di istruzioni o una stored procedure **seleziona**, **UPDATE**, **Inserisci**, e **Elimina** (istruzioni), queste altre istruzioni non influiscono **SQLMoreResults**.  
  
 Per altre informazioni, vedere [più risultati](../../../odbc/reference/develop-app/multiple-results.md).  
  
 Se una ricerca aggiornarla, inserisce o Elimina l'istruzione in un batch di istruzioni non influenza tutte le righe nell'origine dati, **SQLMoreResults** restituisce SQL_SUCCESS. Questo comportamento è diverso da quello di un aggiornamento con ricerca, inserire o eliminare l'istruzione che viene eseguita tramite **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, ovvero Se non influenza tutte le righe nell'origine dati non restituisce SQL_NO_DATA. Se un'applicazione chiama **SQLRowCount** per recuperare il conteggio delle righe dopo una chiamata a **SQLMoreResults** tutte le righe, non interessa **SQLRowCount** restituisce SQL_NO_DATA.  
  
 Per altre informazioni sulla sequenziazione valida delle funzioni di elaborazione dei risultati, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Per altre informazioni sui parametri di output inviati come flusso e SQL_PARAM_DATA_AVAILABLE, vedere [recupero di parametri di Output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="availability-of-row-counts"></a>Disponibilità dei conteggi delle righe  
 Quando un batch contiene più istruzioni di generazione di conteggio righe consecutive, è possibile che questi conteggi delle righe vengono raggruppate nel conteggio di una sola riga. Ad esempio, se un batch contiene cinque istruzioni insert, determinate origini dati sono in grado di restituire cinque i conteggi delle righe singole. Determinati jiné zdroje dat restituiscono solo un conteggio che rappresenta la somma dei conteggi delle righe singole cinque.  
  
 Quando un batch contiene una combinazione di istruzioni di generazione di conteggio delle righe e di generazione di set di risultati, i conteggi delle righe possono o potrebbe non essere disponibili a tutti. Il comportamento del driver per quanto riguarda la disponibilità dei conteggi delle righe viene enumerato nel tipo di informazioni di SQL_BATCH_ROW_COUNT disponibile tramite una chiamata a **SQLGetInfo**. Ad esempio, si supponga che il batch contiene un **selezionate**, seguito da due **Inserisci**s e un altro **selezionare**. Quindi, sono possibili i casi seguenti:  
  
-   Il conteggio delle righe corrispondenti ai due **Inserisci** istruzioni non sono affatto disponibili. La prima chiamata a **SQLMoreResults** verrà è posizionato sul set di risultati del secondo **seleziona** istruzione.  
  
-   Il conteggio delle righe corrispondenti ai due **Inserisci** istruzioni sono disponibili singolarmente. (Una chiamata a **SQLGetInfo** non restituisce il bit SQL_BRC_ROLLED_UP per il tipo di informazioni SQL_BATCH_ROW_COUNT.) La prima chiamata a **SQLMoreResults** verrà è posizionato sul numero di riga del primo **Inserisci**, e la seconda chiamata verrà posizionato sul numero di riga del secondo **Inserisci**. La terza chiamata a **SQLMoreResults** verrà è posizionato sul set di risultati del secondo **seleziona** istruzione.  
  
-   Il conteggio delle righe corrispondenti ai due **inserisce** vengono raggruppate in un conteggio di singola riga che è disponibile. (Una chiamata a **SQLGetInfo** restituisce il SQL_BRC_ROLLED_UP bit per il tipo di informazioni SQL_BATCH_ROW_COUNT.) La prima chiamata a **SQLMoreResults** verrà è posizionato sul conteggio delle righe di roll-up e la seconda chiamata a **SQLMoreResults** verrà è posizionato sul set di risultati del secondo **selezionare**.  
  
 Determinati driver di rendere disponibili solo per i batch espliciti e non per le stored procedure i conteggi delle righe.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Annullare l'elaborazione di istruzione|[Funzione SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Imposta il recupero di un blocco di dati o lo scorrimento di un risultato|[Funzione SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Il recupero di una singola riga o un blocco di dati in una direzione di tipo forward-only|[Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Durante il recupero o parte di una colonna di dati|[Funzione SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recupero di parametri di output tramite SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
