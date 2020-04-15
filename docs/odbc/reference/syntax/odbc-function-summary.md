---
title: Riepilogo delle funzioni ODBC - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10cc7880cf941a1490f963e21e8b44bc91db215
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298922"
---
# <a name="odbc-function-summary"></a>Riepilogo delle funzioni ODBC
Nella tabella seguente sono elencate le funzioni ODBC, raggruppate per tipo di attività, e include la designazione di conformità e una breve descrizione dello scopo di ogni funzione. Per ulteriori informazioni sulle designazioni di conformità, vedere [ODBC e l'interfaccia della riga di comando standard](../../../odbc/reference/odbc-and-the-standard-cli.md). Per ulteriori informazioni sulla sintassi e la semantica per ogni funzione, vedere [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Un'applicazione può chiamare la funzione **SQLGetInfo** per ottenere informazioni di conformità su un driver. Per ottenere informazioni sul supporto per una funzione specifica in un driver, un'applicazione può chiamare **SQLGetFunctions**.  
  
|Attività|Nome della funzione|Conformità|Scopo|  
|----------|-------------------|-----------------|-------------|  
|Connessione a un'origine dati|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|L'ISO 92|Ottiene un handle di ambiente, connessione, istruzione o descrittore.|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|L'ISO 92|Si connette a un driver specifico in base al nome dell'origine dati, all'ID utente e alla password.|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|Si connette a un driver specifico in base alla stringa di connessione o richiede che Gestione Driver e driver visualizzano le finestre di dialogo di connessione per l'utente.|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|Restituisce livelli successivi di attributi di connessione e valori di attributo validi. Quando è stato specificato un valore per ogni attributo di connessione, si connette all'origine dati.|  
|Recupero di informazioni su un driver e un'origine dati|[SqlDataSourcesSQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|L'ISO 92<br /><br /> ODBC|Restituisce l'elenco delle origini dati disponibili.<br /><br /> Restituisce l'elenco dei driver installati e dei relativi attributi.|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|L'ISO 92|Restituisce informazioni su un driver e un'origine dati specifici.|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|L'ISO 92|Restituisce le funzioni di driver supportate.|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|L'ISO 92|Restituisce informazioni sui tipi di dati supportati.|  
|Impostazione e recupero degli attributi del driver|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|L'ISO 92<br /><br /> L'ISO 92|Imposta un attributo di connessione.<br /><br /> Restituisce il valore di un attributo di connessione.|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|L'ISO 92|Imposta un attributo di ambiente.|  
||[SQLGetEnvAttr (Informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|L'ISO 92|Restituisce il valore di un attributo di ambiente.|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|L'ISO 92|Imposta un attributo di istruzione.|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|L'ISO 92|Restituisce il valore di un attributo di istruzione.|  
|Impostazione e recupero dei campi descrittore|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|L'ISO 92<br /><br /> L'ISO 92|Restituisce il valore di un singolo campo descrittore.<br /><br /> Restituisce i valori di più campi descrittore.|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|L'ISO 92|Imposta un singolo campo descrittore.|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|L'ISO 92|Imposta più campi descrittore.|  
||[SQLCopyDesc (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlcopydesc-function.md)|L'ISO 92|Copia le informazioni sul descrittore da un handle di descrittore a un altro.|  
|Preparazione delle richieste SQL|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|L'ISO 92|Prepara un'istruzione SQL per un'esecuzione successiva.|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|Assegna l'archiviazione per un parametro in un'istruzione SQL.|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|L'ISO 92|Restituisce il nome del cursore associato a un handle di istruzione.|  
||[SQLSetCursorName (Nome cursore)](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|L'ISO 92|Specifica un nome di cursore.|  
||[Opzioni SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|Imposta le opzioni che controllano il comportamento del cursore.|  
|Invio di richieste|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|L'ISO 92<br /><br /> L'ISO 92|Esegue un'istruzione preparata.<br /><br /> Esegue un'istruzione.|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|Restituisce il testo di un'istruzione SQL come tradotta dal driver.|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|Restituisce la descrizione per un parametro specifico in un'istruzione.|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|L'ISO 92|Restituisce il numero di parametri in un'istruzione.|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|L'ISO 92|Utilizzato insieme a **SQLPutData** per fornire i dati dei parametri in fase di esecuzione. (Utile per i valori di dati lunghi.)|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|L'ISO 92|Invia parte o tutto un valore di dati per un parametro. (Utile per i valori di dati lunghi.)|  
|Recupero di risultati e informazioni sui risultati|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|L'ISO 92<br /><br /> L'ISO 92|Restituisce il numero di righe interessate da una richiesta di inserimento, aggiornamento o eliminazione.<br /><br /> Restituisce il numero di colonne nel set di risultati.|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|L'ISO 92|Descrive una colonna nel set di risultati.|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|L'ISO 92|Descrive gli attributi di una colonna nel set di risultati.|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|L'ISO 92|Assegna l'archiviazione per una colonna di risultati e specifica il tipo di dati.|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|L'ISO 92|Restituisce più righe di risultati.|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|L'ISO 92|Restituisce le righe dei risultati scorrevoli.|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|L'ISO 92|Restituisce parte o tutta una colonna di una riga di un set di risultati. (Utile per i valori di dati lunghi.)|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|Posiziona un cursore all'interno di un blocco di dati recuperato e consente a un'applicazione di aggiornare i dati nel set di righe o di aggiornare o eliminare i dati nel set di risultati.|  
||[Sqlbulkoperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|Esegue inserimenti in blocco e operazioni di segnalibro in blocco, inclusi i segnalibri, l'eliminazione e il recupero in base al segnalibro.|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|Determina se sono disponibili più set di risultati e, in caso affermativo, inizializza l'elaborazione per il set di risultati successivo.|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|L'ISO 92|Restituisce informazioni diagnostiche aggiuntive (un singolo campo della struttura dei dati di diagnostica).|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|L'ISO 92|Restituisce informazioni diagnostiche aggiuntive (più campi della struttura dei dati di diagnostica).|  
|Recupero di informazioni sulle tabelle di sistema dell'origine dati (funzioni di catalogo)Obtaining information about the data source's system tables (catalog functions)|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> Apri gruppo|Restituisce un elenco di colonne e privilegi associati per una o più tabelle.<br /><br /> Restituisce l'elenco dei nomi di colonna nelle tabelle specificate.|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|Restituisce un elenco di nomi di colonna che costituiscono chiavi esterne, se esistono per una tabella specificata.|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|Restituisce l'elenco dei nomi di colonna che costituiscono la chiave primaria di una tabella.|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|Restituisce l'elenco dei parametri di input e output, nonché le colonne che costituiscono il set di risultati per le procedure specificate.|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|Restituisce l'elenco dei nomi di routine archiviati in un'origine dati specifica.|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|Apri gruppo|Restituisce informazioni sul set ottimale di colonne che identifica in modo univoco una riga in una tabella specificata o sulle colonne che vengono aggiornate automaticamente quando qualsiasi valore nella riga viene aggiornato da una transazione.|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|L'ISO 92|Restituisce statistiche su una singola tabella e sull'elenco di indici associati alla tabella.|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|Restituisce un elenco di tabelle e i privilegi associati a ogni tabella.|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|Apri gruppo|Restituisce l'elenco dei nomi di tabella archiviati in un'origine dati specifica.|  
|Terminazione di un'istruzione|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|L'ISO 92|Termina l'elaborazione dell'istruzione, elimina i risultati in sospeso e, facoltativamente, libera tutte le risorse associate all'handle dell'istruzione.|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|L'ISO 92|Chiude un cursore aperto su un handle di istruzione.|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|L'ISO 92|Annulla l'elaborazione di un'istruzione.|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|Annulla l'elaborazione di un'istruzione o di una connessione.|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|L'ISO 92|Esegue il commit o il rollback di una transazione.|  
|Interruzione di una connessione|[Sqldisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|L'ISO 92<br /><br /> L'ISO 92|Chiude la connessione.<br /><br /> Rilascia un handle di ambiente, connessione, istruzione o descrittore.|
