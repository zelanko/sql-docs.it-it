---
description: Funzioni API del livello di base (driver ODBC per Oracle)
title: Funzioni API di livello principale (driver ODBC per Oracle) | Microsoft Docs
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
ms.openlocfilehash: c0940dd9fbabc02a5fd384208b2dcd4803f4f24a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471653"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funzioni API del livello di base (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le funzioni a questo livello costituiscono il livello minimo di conformità dell'interfaccia per i driver ODBC.  
  
|Funzione API|Note|  
|------------------|-----------|  
|**SQLAllocConnect**|Alloca memoria per un handle di connessione, *HDBC*, all'interno dell'ambiente identificato da *HENV*. Gestione driver elabora questa chiamata e chiama la funzione **SQLAllocConnect** del driver ogni volta che viene chiamato **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect** .|  
|**SQLAllocEnv**|Visualizza una finestra di dialogo che specifica il requisito per il software client Oracle e quindi restituisce SQL_NULL_HANDLE. Se il software client Oracle non è installato, questa funzione alloca memoria per un handle di ambiente, *HENV*, e Inizializza l'interfaccia a livello di chiamata ODBC per l'utilizzo da parte di un'applicazione.|  
|**SQLAllocStmt**|Alloca memoria per un handle di istruzione e associa l'handle di istruzione alla connessione specificata da hdbc. Gestione driver passa questa chiamata al driver, che alloca la memoria per la struttura hstmt.|  
|**SQLBindCol**|Assegna lo spazio di archiviazione per una colonna risultato e specifica il tipo del risultato.|  
|**SQLCancel**|Annulla l'elaborazione in un handle di istruzione, hstmt. In alcuni casi, Oracle non consente l'annullamento di un'istruzione in esecuzione. Ciò significa che un'istruzione in esecuzione continuerà fino a quando Oracle non completerà il processo, a quel punto i risultati delle istruzioni verranno annullati dal driver ODBC per Oracle.|  
|**SQLColAttributes**|Restituisce informazioni sul descrittore per una colonna in un set di risultati. Le informazioni sul descrittore vengono restituite come una stringa di caratteri, un valore dipendente dal descrittore a 32 bit o un valore integer.|  
|**SQLConnect**|Consente di connettersi a un'origine dati. Per utilizzare l'autenticazione del sistema operativo Oracle, specificare "/" come parametro *szUID* e "" come parametro *szAuthStr* .|  
|**SQLDescribeCol**|Restituisce il nome, il tipo, la precisione, la scala e il supporto di valori null della colonna di risultati specificata. **Nota: SQLDescribeCol** segnala le colonne calcolate come SQL_VARCHAR.|  
|**SQLDisconnect**|Chiude una connessione. Se il pool di connessioni è abilitato per un ambiente condiviso e un'applicazione chiama **SQLConnect** in una connessione in tale ambiente, la connessione viene restituita al pool di connessioni ed è ancora disponibile per altri componenti che utilizzano lo stesso ambiente condiviso.|  
|**SQLError**|Restituisce informazioni sull'errore o sullo stato dell'ultimo errore. Il driver gestisce uno stack o un elenco di errori che possono essere restituiti per gli argomenti *HSTMT*, *HDBC*e *HENV* , a seconda del modo in cui viene effettuata la chiamata a **SQLError** . La coda degli errori viene scaricata dopo ogni istruzione. In genere viene recuperato un messaggio di errore Oracle ed è altrimenti vuoto.|  
|**SQLExecDirect**|Esegue una nuova istruzione SQL non preparata. Il driver utilizza i valori correnti delle variabili del marcatore di parametro se nell'istruzione sono presenti parametri. Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette. Se, ad esempio, il database contiene una tabella denominata *My Table* e il campo campo *My*, racchiudere ogni elemento dell'identificatore in modo analogo al seguente:<br /><br /> Selezionare \` la tabella \` . \`My Field1 \` ,; \` Tabella \` . \` Field2 \` dalla \` tabella\`|  
|**SQLExecute**|Esegue un'istruzione SQL preparata (un'istruzione già preparata da **SQLPrepare**). Il driver utilizza i valori correnti delle variabili del marcatore di parametro se nell'istruzione sono presenti parametri.|  
|**SQLFetch**|Recupera una riga da un set di risultati nei percorsi specificati dalle chiamate precedenti a **SQLBindCol**. Prepara il driver per una chiamata a **SQLGetData** per le colonne non vincolate.|  
|**SQLFreeConnect**|Rilascia un handle di connessione e libera tutta la memoria allocata per l'handle.|  
|**SQLFreeEnv**|Chiude il driver ODBC per Oracle e rilascia tutta la memoria associata al driver.|  
|**SQLFreeStmt**|Arresta l'elaborazione associata a un hstmt specifico, chiude tutti i cursori aperti associati a hstmt, Elimina i risultati in sospeso e, facoltativamente, libera tutte le risorse associate all'handle di istruzione.|  
|**SQLGetCursorName**|Restituisce il nome del cursore associato al hstmt specificato.|  
|**SQLNumResultCols**|Restituisce il numero di colonne in un cursore del set di risultati.|  
|**SQLPrepare**|Prepara un'istruzione SQL pianificando come ottimizzare ed eseguire l'istruzione. L'istruzione SQL viene compilata per l'esecuzione da **SQLExecDirect**.<br /><br /> Se i nomi di tabella, vista o campo contengono spazi, racchiudere i nomi tra virgolette. Se, ad esempio, il database contiene una tabella denominata *My Table* e il campo campo *My*, racchiudere ogni elemento dell'identificatore nel modo seguente:<br /><br /> Selezionare \` la tabella \` . \` Campo personale \` della \` tabella\`<br /><br /> Per informazioni sull'utilizzo dei set di risultati contenenti matrici come parametri formali, vedere [restituzione di parametri di matrice da stored procedure](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle non fornisce un modo per determinare il numero di righe in un set di risultati fino a quando non viene recuperato l'ultima riga, pertanto viene restituito-1.|  
|**SQLSetCursorName**|Associa un nome di cursore a un handle di istruzione attivo, *HSTMT*.|  
|**SQLSetParam**|Sostituito da SQLBindParameter in ODBC 2. *x*.|  
|**SQLTransact**|Richiede un'operazione di commit o di rollback per tutte le operazioni attive in tutti gli handle di istruzione (hstmt) associati a una connessione o per tutte le connessioni associate all'handle di ambiente, *HENV*. Se un commit ha esito negativo in modalità manuale, la transazione rimane attiva. è possibile scegliere di eseguire il rollback della transazione o di ripetere l'operazione di commit. Se un'operazione di commit ha esito negativo in modalità di transazione automatica, viene eseguito il rollback automatico della transazione. la transazione non può essere inattiva.|
