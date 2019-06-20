---
title: Funzioni API del livello (Driver ODBC per Oracle) di base | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2e77ffd4fe892bc2f3d9a944c79d6b702d5e671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66354580"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funzioni API del livello di base (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Funzioni a questo livello costituiscono il livello minimo di conformità di interfaccia per i driver ODBC.  
  
|Funzione dell'API|Note|  
|------------------|-----------|  
|**SQLAllocConnect**|Alloca memoria per un handle di connessione *hdbc*, all'interno dell'ambiente identificato dal *henv*. Gestione Driver elabora questa chiamata e il driver chiama **SQLAllocConnect** funzione ogni qualvolta **SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect** viene chiamato.|  
|**SQLAllocEnv**|Visualizza una finestra di dialogo che specifica il requisito per il software Client Oracle e quindi restituisce SQL_NULL_HANDLE. Se non è installato il software Client Oracle, questa funzione alloca memoria per un handle di ambiente *henv*e la inizializza l'interfaccia ODBC a livello di chiamata usata da un'applicazione.|  
|**SQLAllocStmt**|Alloca memoria per un handle di istruzione e associa la connessione specificata dall'oggetto hdbc l'handle di istruzione. Gestione Driver passa la chiamata al driver, che consente di allocare la memoria per la struttura hstmt.|  
|**SQLBindCol**|Assegna lo spazio di archiviazione per una colonna di risultati e specifica il tipo del risultato.|  
|**SQLCancel**|Annulla l'elaborazione su un handle di istruzione, hstmt. In alcuni casi, Oracle non supporta l'annullamento di un'istruzione in esecuzione. Ciò significa che un'istruzione in esecuzione continuerà fino a quando non Oracle completa il processo, momento in cui i risultati delle istruzioni vengono annullati dal Driver ODBC per Oracle.|  
|**SQLColAttributes**|Restituisce informazioni sul descrittore per una colonna in un set di risultati. Informazioni sul descrittore viene restituiti come una stringa di caratteri, un valore di dipendente dal descrittore di 32 bit o un valore intero.|  
|**SQLConnect**|Si connette a un'origine dati. Per utilizzare l'autenticazione del sistema operativo Oracle, specificare "/" come il *szUID* parametro e "" come il *szAuthStr* parametro.|  
|**SQLDescribeCol**|Restituisce il nome, tipo, precisione, scala e supporto di valori null della colonna di risultati specificato. **Nota:  SQLDescribeCol** riporta le colonne calcolate come SQL_VARCHAR.|  
|**SQLDisconnect**|Chiude una connessione. Se il pool di connessioni è abilitato per un ambiente condiviso e un'applicazione chiama **SQLDisconnect** su una connessione in tale ambiente, viene restituita al pool di connessioni e ancora disponibile ad altri componenti tramite la connessione lo stesso ambiente condiviso.|  
|**SQLError**|Restituisce le informazioni di stato o di errore sull'ultimo errore. Il driver gestisce un stack o un elenco di errori che possono essere restituite per il *hstmt*, *hdbc*, e *henv* argomenti, a seconda di come la chiamata a **SQLError**  viene eseguita. Nella coda degli errori deve essere scaricata dopo ogni istruzione. In genere recupera un messaggio di errore Oracle e in caso contrario, è vuoto.|  
|**SQLExecDirect**|Esegue un'istruzione SQL nuovo, non preparata. Il driver utilizza i valori correnti delle variabili di marcatore di parametro, se sono presenti parametri nell'istruzione. Se la tabella, vista o i nomi dei campi contengono spazi, racchiudere i nomi tra backup preventivo contrassegni. Ad esempio, se il database contiene una tabella denominata *My Table* e il campo *My Field*, racchiudere ogni elemento dell'identificatore come segue:<br /><br /> Selezionare \`tabella\`. \`My Field1\`, \`Della tabella\`.\` My Field2\` FROM \`mia tabella\`|  
|**SQLExecute**|Esegue un'istruzione SQL preparata (un'istruzione già preparata da **SQLPrepare**). Il driver utilizza i valori correnti delle variabili di marcatore di parametro, se sono presenti parametri nell'istruzione.|  
|**SQLFetch**|Recupera una riga da un set di risultati in posizioni specificate dalle chiamate precedenti a **SQLBindCol**. Prepara il driver per una chiamata a **SQLGetData** per le colonne non associate.|  
|**SQLFreeConnect**|Rilascia un handle di connessione e libera tutta la memoria allocata per l'handle.|  
|**SQLFreeEnv**|Chiude il Driver ODBC per Oracle e libera tutta la memoria associata al driver.|  
|**SQLFreeStmt**|Arresta elaborazione associata a un oggetto specifico hstmt, chiude tutti i cursori aperti associati hstmt, ignora risultati in sospeso e, facoltativamente, rilascia tutte le risorse associate all'handle di istruzione.|  
|**SQLGetCursorName**|Restituisce il nome del cursore associato hstmt specificato.|  
|**SQLNumResultCols**|Restituisce il numero di colonne in un cursore del set di risultati.|  
|**SQLPrepare**|Prepara un'istruzione SQL, pianificare come ottimizzare ed eseguire l'istruzione. L'istruzione SQL viene compilata per l'esecuzione dal **SQLExecDirect**.<br /><br /> Se la tabella, vista o i nomi dei campi contengono spazi, racchiudere i nomi tra backup preventivo contrassegni. Ad esempio, se il database contiene una tabella denominata *My Table* e il campo *My Field*, racchiudere ogni elemento dell'identificatore, come indicato di seguito:<br /><br /> Selezionare \`della tabella\`.\` Il campo relativo alla\` FROM \`mia tabella\`<br /><br /> Per informazioni sull'uso di set di risultati contenenti matrici di parametri formali, vedere [restituzione di parametri di matrice dalle Stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle non fornisce un modo per determinare il numero di righe in un risultato impostata fino a quando non dopo il recupero dell'ultima riga, pertanto, restituisce -1.|  
|**SQLSetCursorName**|Associa un handle di istruzione attiva, un nome di cursore *hstmt*.|  
|**SQLSetParam**|Sostituito da SQLBindParameter in ODBC 2. *x*.|  
|**SQLTransact**|Richiede un'operazione di commit o rollback per tutte le operazioni attive in tutti gli handle di istruzione (HSTMT) associati a una connessione o per tutte le connessioni associate l'handle di ambiente *henv*. Se un'operazione di commit ha esito negativo quando è in modalità manuale, la transazione rimane attiva; è possibile scegliere di rollback della transazione o ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo quando è in modalità di transazione automatica, il rollback della transazione automaticamente. la transazione non può essere inattiva.|
