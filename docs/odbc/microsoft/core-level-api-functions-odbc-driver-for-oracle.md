---
title: Funzioni API di livello principale (driver ODBC per Oracle) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281021"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funzioni API del livello di base (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello costituiscono il livello minimo di conformità dell'interfaccia per i driver ODBC.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLAllocConnect (connessione a questo errore)**|Alloca memoria per un handle di connessione, *hdbc*, all'interno dell'ambiente identificato da *henv*. Gestione Driver elabora questa chiamata e chiama la funzione **SQLAllocConnect** del driver ogni volta che viene chiamato **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect** .|  
|**SQLAllocEnv (informazioni in lingua inglese)**|Visualizza una finestra di dialogo che specifica il requisito per il software Oracle Client, quindi restituisce SQL_NULL_HANDLE. Se il software Oracle Client non è installato, questa funzione alloca memoria per un handle di ambiente, *henv*, e inizializza l'interfaccia a livello di chiamata ODBC per l'utilizzo da parte di un'applicazione.|  
|**Istruzione SQLAllocStmt (informazioni in lingua inglese)**|Alloca memoria per un handle di istruzione e associa l'handle di istruzione alla connessione specificata da hdbc. Gestione Driver passa questa chiamata al driver, che alloca la memoria per la struttura hstmt.|  
|**SQLBindCol**|Assegna spazio di archiviazione per una colonna di risultati e specifica il tipo del risultato.|  
|**SQLCancel**|Annulla l'elaborazione su un handle di istruzione, hstmt. In alcuni casi, Oracle non consente l'annullamento di un'istruzione in esecuzione. Ciò significa che un'istruzione in esecuzione continuerà fino a quando Oracle completa il processo, in cui i risultati delle istruzioni vengono annullati dal driver ODBC per Oracle.|  
|**ATTRIBUTI SQLCol**|Restituisce informazioni sul descrittore per una colonna in un set di risultati. Le informazioni sul descrittore vengono restituite come stringa di caratteri, come valore dipendente dal descrittore a 32 bit o come valore intero.|  
|**SQLConnect**|Si connette a un'origine dati. Per utilizzare l'autenticazione del sistema operativo Oracle, specificare "/" come parametro *szUID* e "" come parametro *szAuthStr.*|  
|**SQLDescribeCol**|Restituisce il nome, il tipo, la precisione, la scala e il supporto di valori Null della colonna dei risultati specificata. **Nota: SQLDescribeCol** segnala le colonne calcolate come SQL_VARCHAR.|  
|**Sqldisconnect**|Chiude una connessione. Se il pool di connessioni è abilitato per un ambiente condiviso e un'applicazione chiama **SQLDisconnect** su una connessione in tale ambiente, la connessione viene restituita al pool di connessioni ed è ancora disponibile per altri componenti che utilizzano lo stesso ambiente condiviso.|  
|**Sqlerror**|Restituisce informazioni sull'errore o sullo stato relative all'ultimo errore. Il driver gestisce uno stack o un elenco di errori che possono essere restituiti per il *hstmt*, *hdbc*, e *henv* argomenti, a seconda di come viene effettuata la chiamata a **SQLError.** La coda degli errori viene scaricata dopo ogni istruzione. In genere recupera un messaggio di errore Oracle ed è altrimenti vuoto.|  
|**SQLExecDirect**|Esegue una nuova istruzione SQL non preparata. Il driver utilizza i valori correnti delle variabili del marcatore di parametro se esistono parametri nell'istruzione. Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette rovesciate. Ad esempio, se il database contiene una tabella denominata *Tabella personale* e il campo *Campo personale*, racchiudere ogni elemento dell'identificatore in questo modo:<br /><br /> SELEZIONARE \`\`Tabella personale . \`Il mio\`Campo1 ,; \`Il\`mio tavolo . \`Il mio\` \`Field2 DA My Table\`|  
|**SQLExecute**|Esegue un'istruzione SQL preparata (un'istruzione già preparata da **SQLPrepare**). Il driver utilizza i valori correnti delle variabili del marcatore di parametro se esistono parametri nell'istruzione.|  
|**SQLFetch**|Recupera una riga da un set di risultati nelle posizioni specificate dalle chiamate precedenti a **SQLBindCol**. Prepara il driver per una chiamata a **SQLGetData** per le colonne non associate.|  
|**SQLFreeConnect (informazioni in lingua inglese)**|Rilascia un handle di connessione e libera tutta la memoria allocata per l'handle.|  
|**SQLFreeEnv (informazioni in lingua inglese)**|Chiude il driver ODBC per Oracle e rilascia tutta la memoria associata al driver.|  
|**SQLFreeStmt**|Interrompe l'elaborazione associata a un hstmt specifico, chiude tutti i cursori aperti associati a hstmt, elimina i risultati in sospeso e, facoltativamente, libera tutte le risorse associate all'handle dell'istruzione.|  
|**SQLGetCursorName**|Restituisce il nome del cursore associato all'oggetto hstmt specificato.|  
|**SQLNumResultCols**|Restituisce il numero di colonne in un cursore del set di risultati.|  
|**SQLPrepare**|Prepara un'istruzione SQL pianificando come ottimizzare ed eseguire l'istruzione. L'istruzione SQL viene compilata per l'esecuzione da **SQLExecDirect**.<br /><br /> Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette rovesciate. Ad esempio, se il database contiene una tabella denominata *Tabella personale* e il campo *Campo personale*, racchiudere ogni elemento dell'identificatore come segue:<br /><br /> SELEZIONARE \`\`Tabella personale . \`Il\` mio \`campo da Il mio tavolo\`<br /><br /> Per informazioni sull'utilizzo di set di risultati contenenti matrici come parametri formali, vedere [Restituzione di parametri di matrice da stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle non fornisce un modo per determinare il numero di righe in un set di risultati fino a dopo aver recuperato l'ultima riga, pertanto restituisce -1.|  
|**SQLSetCursorName (Nome cursore)**|Associa un nome di cursore a un handle di istruzione attivo, *hstmt*.|  
|**SQLSetParam (informazioni in lingua inglese)**|Sostituito da SQLBindParameter in ODBC 2. *x*.|  
|**SQLTransact (transazione SQLTransact)**|Richiede un'operazione di commit o rollback per tutte le operazioni attive su tutti gli handle di istruzione (hstmt) associati a una connessione o per tutte le connessioni associate all'handle di ambiente, *henv*. Se un commit ha esito negativo in modalità manuale, la transazione rimane attiva; è possibile scegliere di eseguire il rollback della transazione o ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo in modalità di transazione automatica, viene eseguito automaticamente il rollback della transazione. la transazione non può essere inattiva.|
