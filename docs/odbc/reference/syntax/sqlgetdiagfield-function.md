---
title: Funzione SQLGetDiagField . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285431"
---
# <a name="sqlgetdiagfield-function"></a>Funzione SQLGetDiagField

**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetDiagField** restituisce il valore corrente di un campo di un record della struttura di dati di diagnostica (associata a un handle specificato) che contiene informazioni su errori, avvisi e stato.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp

SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Identificatore del tipo di handle che descrive il tipo di handle per il quale è necessaria la diagnostica. I possibili valori sono i seguenti:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN handle viene utilizzato solo da Gestione Driver e dal driver. Le applicazioni non devono utilizzare questo tipo di handle. Per ulteriori informazioni su SQL_HANDLE_DBC_INFO_TOKEN, vedere Sviluppo del [riconoscimento](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)del pool di connessioni in un driver ODBC .  
  
 *Handle*  
 [Ingresso] Handle per la struttura dei dati di diagnostica, del tipo indicato da *HandleType*. Se *HandleType* è SQL_HANDLE_ENV, *Handle* può essere un handle di ambiente condiviso o non condiviso.  
  
 *RecNumber*  
 [Ingresso] Indica il record di stato da cui l'applicazione cerca informazioni. I record di stato sono numerati a partire da 1. Se l'argomento *DiagIdentifier* indica un campo dell'intestazione di diagnostica, *RecNumber* viene ignorato. In caso contrario, dovrebbe essere maggiore di 0.  
  
 *DiagIdentifier (Identificatore diag)*  
 [Ingresso] Indica il campo della diagnostica il cui valore deve essere restituito. Per ulteriori informazioni, vedere la sezione "Argomento*DiagIdentifier"* in "Commenti".  
  
 *DiagInfoPtr*  
 [Uscita] Puntatore a un buffer in cui restituire le informazioni di diagnostica. Il tipo di dati dipende dal valore di *DiagIdentifier*. Se *DiagInfoPtr* è un tipo integer, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione, poiché alcuni driver possono scrivere solo il bit inferiore a 32 o 16 bit di un buffer e lasciare invariato il bit di ordine superiore.  
  
 Se *DiagInfoPtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *DiagInfoPtr*.  
  
 *BufferLength*  
 [Ingresso] Se *DiagIdentifier* è una diagnostica definita da ODBC e *DiagInfoPtr* punta a una stringa \*di caratteri o a un buffer binario, questo argomento deve essere la lunghezza di *DiagInfoPtr*. Se *DiagIdentifier* è un campo \*definito da ODBC e *DiagInfoPtr* è un numero intero, *BufferLength* viene ignorato. Se il valore in * \*DiagInfoPtr* è una stringa Unicode (quando si chiama **SQLGetDiagFieldW**), l'argomento *BufferLength* deve essere un numero pari.  
  
 Se *DiagIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo in Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i seguenti valori:  
  
-   Se *DiagInfoPtr* è un puntatore a una stringa di caratteri, *BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *DiagInfoPtr* è un puntatore a un buffer binario, l'applicazione inserisce il risultato della macro SQL_LEN_BINARY_ATTR(*length*) in *BufferLength*. In questo modo un valore negativo in *BufferLength*.  
  
-   Se *DiagInfoPtr* è un puntatore a un valore diverso da una stringa di caratteri o una stringa binaria, *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se * \*DiagInfoPtr* contiene un tipo di dati a lunghezza fissa, *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, a seconda dei casi.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il numero \*di byte necessari per il carattere di terminazione null) disponibile per la restituzione in *DiagInfoPtr*, per i dati di tipo carattere. Se il numero di byte disponibili da restituire è maggiore \*o uguale a *BufferLength*, il testo in *DiagInfoPtr* viene troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLGetDiagField** non registra record di diagnostica per se stesso. Utilizza i seguenti valori restituiti per segnalare il risultato della propria esecuzione:  
  
-   SQL_SUCCESS: la funzione ha restituito correttamente le informazioni di diagnostica.  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr* era troppo piccolo per contenere il campo di diagnostica richiesto. Pertanto, i dati nel campo di diagnostica sono stati troncati. Per determinare che si è verificato un troncamento, l'applicazione deve confrontare *BufferLength* con il numero effettivo di byte disponibili, che viene scritto in*StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: l'handle indicato da *HandleType* e *Handle* non è un handle valido.  
  
-   SQL_ERROR: si è verificato uno dei seguenti:  
  
    -   *L'argomento DiagIdentifier* non è uno dei valori validi.  
  
    -   *L'argomento DiagIdentifier* è stato SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE o SQL_DIAG_ROW_COUNT, ma *Handle* non è un handle di istruzione. (Gestione Driver restituisce questa diagnostica.)  
  
    -   *L'argomento RecNumber* era negativo o 0 quando *DiagIdentifier* indicava un campo da un record di diagnostica. *RecNumber* viene ignorato per i campi di intestazione.  
  
    -   Il valore richiesto era una stringa di caratteri e *BufferLength* minore di zero.  
  
    -   Quando si utilizza la notifica asincrona, l'operazione asincrona sull'handle non è stata completata.  
  
-   SQL_NO_DATA: *RecNumber* era maggiore del numero di record di diagnostica esistenti per l'handle specificato in *Handle.* La funzione restituisce inoltre SQL_NO_DATA per qualsiasi *RecNumber* positivo se non sono presenti record di diagnostica per *Handle*.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere SQLGetDiagField per raggiungere uno dei tre obiettivi:An application typically calls **SQLGetDiagField** to accomplish one of three goals:  
  
1.  Per ottenere informazioni specifiche sull'errore o sull'avviso quando una chiamata di funzione ha restituito SQL_ERROR o SQL_SUCCESS_WITH_INFO (o SQL_NEED_DATA per la funzione **SQLBrowseConnect).**  
  
2.  Per determinare il numero di righe nell'origine dati interessate quando le operazioni di inserimento, eliminazione o aggiornamento sono state eseguite con una chiamata a **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos** (dal campo di intestazione SQL_DIAG_ROW_COUNT) o per determinare il numero di righe presenti nel cursore aperto corrente, se il driver può fornire queste informazioni (dal campo di intestazione SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Per determinare quale funzione è stata eseguita da una chiamata a **SQLExecDirect** o **SQLExecute** (dai campi di intestazione SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Qualsiasi funzione ODBC può registrare zero o più record di diagnostica ogni volta che viene chiamata, in modo che un'applicazione può chiamare **SQLGetDiagField** dopo qualsiasi chiamata di funzione ODBC. Non esiste alcun limite al numero di record di diagnostica che possono essere archiviati contemporaneamente. **SQLGetDiagField** recupera solo le informazioni di diagnostica associate più di recente alla struttura di dati di diagnostica specificata nel *Handle* argomento. Se l'applicazione chiama una funzione ODBC diversa da **SQLGetDiagField** o **SQLGetDiagRec**, tutte le informazioni diagnostiche di una chiamata precedente con lo stesso handle andranno perse.  
  
 Un'applicazione può eseguire la scansione di tutti i record di diagnostica incrementando *RecNumber*, purché **SQLGetDiagField** restituisca SQL_SUCCESS. Il numero di record di stato è indicato nel campo di intestazione SQL_DIAG_NUMBER. Le chiamate a **SQLGetDiagField** non sono distruttive per i campi di intestazione e record. L'applicazione può chiamare **SQLGetDiagField** in un secondo momento per recuperare un campo da un record, purché una funzione diversa dalle funzioni di diagnostica non è stata chiamata nel frattempo, che pubblicherebbe record sullo stesso handle.  
  
 Un'applicazione può chiamare **SQLGetDiagField** per restituire qualsiasi campo di diagnostica in qualsiasi momento, ad eccezione di SQL_DIAG_CURSOR_ROW_COUNT o SQL_DIAG_ROW_COUNT, che restituirà SQL_ERROR se *Handle* non è un handle di istruzione. Se qualsiasi altro campo di diagnostica non è definito, la chiamata a **SQLGetDiagField** restituirà SQL_SUCCESS (a condizione che non venga rilevata alcun'altra diagnostica) e venga restituito un valore non definito per il campo.  
  
 Per ulteriori informazioni, vedere [Utilizzo di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e Implementazione di [SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 La chiamata a un'API diversa da quella eseguita in modo asincrono genererà HY010 "Errore di sequenza di funzioni". Tuttavia, il record di errore non può essere recuperato prima del completamento dell'operazione asincrona.  
  
## <a name="handletype-argument"></a>Argomento HandleType  
 A ogni tipo di handle possono essere associate informazioni di diagnostica. L'argomento *HandleType* indica il tipo di handle di *Handle*.  
  
 Alcuni campi di intestazione e record non possono essere restituiti per gli handle di ambiente, connessione, istruzione e descrittore. Gli handle per i quali un campo non è applicabile sono indicati nelle sezioni "Campi di intestazione" e "Campi record" seguenti.  
  
 Se *HandleType* è SQL_HANDLE_ENV, *Handle* può essere un handle di ambiente condiviso o non condiviso.  
  
 Nessun campo di diagnostica dell'intestazione specifico del driver deve essere associato a un handle di ambiente.  
  
 Gli unici campi di intestazione di diagnostica definiti per un handle di descrittore sono SQL_DIAG_NUMBER e SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argomento DiagIdentifier  
 Questo argomento indica l'identificatore del campo richiesto dalla struttura dei dati di diagnostica. Se *RecNumber* è maggiore o uguale a 1, i dati nel campo descrivono le informazioni di diagnostica restituite da una funzione. Se *RecNumber* è 0, il campo si trova nell'intestazione della struttura dei dati di diagnostica e pertanto contiene dati relativi alla chiamata di funzione che ha restituito le informazioni di diagnostica, non alle informazioni specifiche.  
  
 I driver possono definire campi di intestazione e record specifici del driver nella struttura dei dati di diagnostica.  
  
 Un'applicazione ODBC 3 *.x* che utilizza un driver ODBC 2 *.x* sarà in grado di chiamare **SQLGetDiagField** solo con un *DiagIdentifier* argomento di SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Tutti gli altri campi di diagnostica restituiranno SQL_ERROR.  
  
## <a name="header-fields"></a>Campi intestazione  
 I campi di intestazione elencati nella tabella seguente possono essere inclusi nell'argomento *DiagIdentifier.*  
  
|DiagIdentifier (Identificatore diag)|Tipo restituito|Valori di codice restituiti|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN (informazioni in lingua inglese)|Questo campo contiene il numero di righe nel cursore. La semantica dipende dai tipi di informazioni **sqlGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 e SQL_STATIC_CURSOR_ATTRIBUTES2, che indicano quali conteggi delle righe sono disponibili per ogni tipo di cursore (nel SQL_CA2_CRC_EXACT e SQL_CA2_CRC_APPROXIMATE bit).<br /><br /> Il contenuto di questo campo viene definito solo per gli handle di istruzione e solo dopo la chiamata a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** . La chiamata a **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_CURSOR_ROW_COUNT su un handle di istruzione diverso restituirà SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|Proprietà SQLCHAR .|Si tratta di una stringa che descrive l'istruzione SQL eseguita dalla funzione sottostante. Per valori specifici, vedere "Valori dei campi Funzione dinamica" più avanti in questa sezione. Il contenuto di questo campo viene definito solo per gli handle di istruzione e solo dopo una chiamata a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults**. La chiamata a **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_DYNAMIC_FUNCTION su un handle di istruzione diverso restituirà SQL_ERROR. Il valore di questo campo non è definito prima di una chiamata a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Si tratta di un codice numerico che descrive l'istruzione SQL eseguita dalla funzione sottostante. Per un valore specifico, vedere "Valori dei campi funzione dinamica" più avanti in questa sezione. Il contenuto di questo campo viene definito solo per gli handle di istruzione e solo dopo una chiamata a **SQLExecute**, **SQLExecDirect**o **SQLMoreResults**. La chiamata a **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_DYNAMIC_FUNCTION_CODE su un handle di istruzione diverso restituirà SQL_ERROR. Il valore di questo campo non è definito prima di una chiamata a **SQLExecute** o **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|Numero di record di stato disponibili per l'handle specificato.|  
|SQL_DIAG_RETURNCODE|VALORE SQLRETURN|Codice restituito dalla funzione. Per un elenco dei codici restituiti, vedere [Codici restituiti](../../../odbc/reference/develop-app/return-codes-odbc.md). Il driver non deve implementare SQL_DIAG_RETURNCODE; è sempre implementato da Gestione Driver. Se non è stata ancora chiamata alcuna funzione su *Handle*, SQL_SUCCESS verrà restituito per SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN (informazioni in lingua inglese)|Numero di righe interessate da un inserimento, eliminazione o aggiornamento eseguito da **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**o **SQLSetPos**. È definito dal driver dopo l'esecuzione di una specifica del *cursore.* Il contenuto di questo campo viene definito solo per gli handle di rendiconto. La chiamata a **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_ROW_COUNT su un handle di istruzione diverso restituirà SQL_ERROR. I dati in questo campo vengono restituiti anche nell'argomento *RowCountPtr* di **SQLRowCount**. I dati in questo campo vengono reimpostati dopo ogni chiamata di funzione non diagnostica, mentre il conteggio delle righe restituito da **SQLRowCount** rimane invariato fino a quando l'istruzione non viene reimpostata sullo stato preparato o allocato.|  
  
## <a name="record-fields"></a>Campi record  
 I campi di record elencati nella tabella seguente possono essere inclusi nell'argomento *DiagIdentifier.*  
  
|DiagIdentifier (Identificatore diag)|Tipo restituito|Valori di codice restituiti|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|Proprietà SQLCHAR .|Stringa che indica il documento che definisce la parte di classe del valore SQLSTATE in questo record. Il valore è "ISO 9075" per tutti i SQLSTATE definiti da Open Group e dall'interfaccia a livello di chiamata ISO. Per SQLSTATEs specifici di ODBC (tutti quelli la cui classe SQLSTATE è "IM"), il valore è "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Se il campo SQL_DIAG_ROW_NUMBER è un numero di riga valido in un set di righe o un set di parametri, questo campo contiene il valore che rappresenta il numero di colonna nel set di risultati o il numero di parametro nel set di parametri. I numeri di colonna del set di risultati iniziano sempre da 1; se questo record di stato si riperca su una colonna di segnalibro, il campo può essere zero. I numeri di parametro iniziano da 1. Ha il valore SQL_NO_COLUMN_NUMBER se il record di stato non è associato a un numero di colonna o un numero di parametro. Se il driver non è in grado di determinare il numero di colonna o il numero di parametro a cui è associato questo record, questo campo ha il valore SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> Il contenuto di questo campo viene definito solo per gli handle di rendiconto.|  
|SQL_DIAG_CONNECTION_NAME|Proprietà SQLCHAR .|Stringa che indica il nome della connessione a cui si riferisce il record di diagnostica. Questo campo è definito dal driver. Per le strutture di dati di diagnostica associate all'handle di ambiente e per la diagnostica che non sono correlate ad alcuna connessione, questo campo è una stringa di lunghezza zero.|  
|SQL_DIAG_MESSAGE_TEXT|Proprietà SQLCHAR .|Un messaggio informativo sull'errore o sull'avviso. Questo campo viene formattato come descritto in [Messaggi di diagnostica](../../../odbc/reference/develop-app/diagnostic-messages.md). Non esiste una lunghezza massima per il testo del messaggio di diagnostica.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Un codice di errore nativo specifico del driver/origine dati. Se non è presente alcun codice di errore nativo, il driver restituisce 0.If there is no native error code, the driver returns 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN (informazioni in lingua inglese)|Questo campo contiene il numero di riga nel set di righe o il numero di parametro nel set di parametri a cui è associato il record di stato. I numeri di riga e i numeri di parametro iniziano con 1. Questo campo ha il valore SQL_NO_ROW_NUMBER se questo record di stato non è associato a un numero di riga o di parametro. Se il driver non è in grado di determinare il numero di riga o di parametro a cui è associato questo record, questo campo ha il valore SQL_ROW_NUMBER_UNKNOWN.<br /><br /> Il contenuto di questo campo viene definito solo per gli handle di rendiconto.|  
|SQL_DIAG_SERVER_NAME|Proprietà SQLCHAR .|Stringa che indica il nome del server a cui si riferisce il record di diagnostica. È uguale al valore restituito per una chiamata a **SQLGetInfo** con l'opzione SQL_DATA_SOURCE_NAME. Per le strutture di dati di diagnostica associate all'handle di ambiente e per la diagnostica che non sono correlate ad alcun server, questo campo è una stringa di lunghezza zero.|  
|SQL_DIAG_SQLSTATE|Proprietà SQLCHAR .|Codice di diagnostica SQLSTATE di cinque caratteri. Per ulteriori informazioni, vedere [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|Proprietà SQLCHAR .|Stringa con lo stesso formato e gli stessi valori validi di SQL_DIAG_CLASS_ORIGIN, che identifica la parte di definizione della parte della sottoclasse del codice SQLSTATE. Gli SQLSTATES specifici di ODBC per cui viene restituito "ODBC 3.0" sono i seguenti:<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY999 HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valori dei campi funzione dinamica  
 Nella tabella seguente vengono descritti i valori di SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE che si applicano a ogni tipo di istruzione SQL eseguita da una chiamata a **SQLExecute** o **SQLExecDirect**. Il driver può aggiungere valori definiti dal driver a quelli elencati.  
  
|Istruzione SQL<br /><br /> Eseguito|Valore di <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valore di <br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-statement*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-statement*|"MODIFICA TABELLA"|SQL_DIAG_ALTER_TABLE|  
|*assertion-definition*|"CREA ASSERTION"|SQL_DIAG_CREATE_ASSERTION|  
|*carattere-set-definizione*|"CREA SET DI CARATTERI"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*definizione delle regole di confronto*|"CREA REGOLE DI CONFRONTO"|SQL_DIAG_CREATE_COLLATION|  
|*definizione di dominion*|"CREA DOMINIO"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|"CREA INDICE"|SQL_DIAG_CREATE_INDEX|  
|*create-table-statement*|"CREA TABELLA"|SQL_DIAG_CREATE_TABLE|  
|*create-view-statement*|"CREA VISTA"|SQL_DIAG_CREATE_VIEW|  
|*specifica del cursore*|"SELEZIONA CURSORE"|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-posizionato*|"CURSORE ELIMINA DINAMICO"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-statement-cercato*|"ELIMINA DOVE"|SQL_DIAG_DELETE_WHERE|  
|*goccia-assertion-statement*|"ELIMINA ASSERZIONE"|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|"ABBANDONA SET DI CARATTERI"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|"REGOLE DI CONFRONTO DI DROP"|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|"ELIMINA DOMINIO"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-statement*|"INDICE DI RILASCIO"|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|"ELIMINA SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|"ELIMINA TABELLA"|SQL_DIAG_DROP_TABLE|  
|*drop-translation-statement*|"TRADUZIONE DI DROP"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|"DROP VIEW" (VISUALIZZA A DISCESA)|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|"GRANT"|SQL_DIAG_GRANT|
|*insert-statement*|"INSERISCI"|SQL_DIAG_INSERT|  
|*Estensione della procedura ODBCODBC-procedure-extension*|"CHIAMA"|SQL_DIAG_ CHIAMATA|  
|*revoke-statement*|"REVOKE"|SQL_DIAG_REVOKE|  
|*schema-definizione*|"CREA SCHEMA"|SQL_DIAG_CREATE_SCHEMA|  
|*traduzione-definizione*|"CREA TRADUZIONE"|SQL_DIAG_CREATE_TRANSLATION|  
|*aggiornare-dichiarazione posizionata*|"CURSORE DI AGGIORNAMENTO DINAMICO"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-ricercato*|"AGGIORNA DOVE"|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*stringa vuota*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>Sequenza di record di stato

 I record di stato vengono posizionati in una sequenza in base al numero di riga e al tipo di diagnostica. Gestione Driver determina l'ordine finale in cui restituire i record di stato che genera. Il driver determina l'ordine finale in cui restituire i record di stato che genera.  
  
 Se i record di diagnostica vengono registrati sia da Gestione Driver che dal driver, Gestione Driver è responsabile dell'ordinazione.  
  
 Se sono presenti due o più record di stato, la sequenza dei record viene determinata prima in base al numero di riga. Le regole seguenti si applicano alla determinazione della sequenza di record di diagnostica per riga:  
  
-   I record che non corrispondono ad alcuna riga vengono visualizzati davanti ai record che corrispondono a una determinata riga, poiché SQL_NO_ROW_NUMBER è definito come -1.  
  
-   I record per i quali il numero di riga è sconosciuto vengono visualizzati davanti a tutti gli altri record, in quanto SQL_ROW_NUMBER_UNKNOWN è definito come -2.  
  
-   Per tutti i record relativi a righe specifiche, i record vengono ordinati in base al valore nel campo SQL_DIAG_ROW_NUMBER. Vengono elencati tutti gli errori e gli avvisi della prima riga interessata, quindi tutti gli errori e gli avvisi della riga successiva interessati e così via.  
  
> [!NOTE]
>  Gestione Driver ODBC 3 *.x* non ordina i record di stato nella coda di diagnostica se SQLSTATE 01S01 (Errore nella riga) viene restituito da un driver *.x* ODBC 2 o se SQLSTATE 01S01 (Errore nella riga) viene restituito da un driver ODBC 3 *.x* quando **SQLExtendedFetch** viene chiamato o **SQLSetPos** viene chiamato su un cursore che è stato posizionato con **SQLExtendedFetch**.  
  
 All'interno di ogni riga, o per tutti i record che non corrispondono a una riga o per cui il numero di riga è sconosciuto, o per tutti i record con un numero di riga uguale a SQL_NO_ROW_NUMBER, il primo record elencato viene determinato utilizzando un set di regole di ordinamento. Dopo il primo record, l'ordine degli altri record che interessano una riga non è definito. Un'applicazione non può presupporre che gli errori precedano gli avvisi dopo il primo record. Le applicazioni devono eseguire la scansione completa della struttura dei dati di diagnostica completa per ottenere informazioni complete su una chiamata non riuscita a una funzione.  
  
 Le regole seguenti vengono utilizzate per determinare il primo record all'interno di una riga. Il record con il rango più alto è il primo record. L'origine di un record (Gestione driver, driver, gateway e così via) non viene considerata durante la classificazione dei record.  
  
-   **Errori** I record di stato che descrivono gli errori hanno la classificazione più alta. Per gli errori di ordinamento vengono applicate le regole seguenti:  
  
    -   I record che indicano un errore di transazione o un possibile errore di transazione superano tutti gli altri record.  
  
    -   Se due o più record descrivono la stessa condizione di errore, sqlSTATEs definiti dalla specifica Open Group CLI (classi da 03 a Hz) superano SQLSTATE e SQLSTATE definiti dal driver.  
  
-   **Valori no data definiti dall'implementazioneImplementation-defined No Data Values** I record di stato che descrivono i valori Nessun dato definiti dal driver (classe 02) hanno il secondo rango più alto.  
  
-   **Avvertenze** I record di stato che descrivono gli avvisi (classe 01) hanno il rango più basso. Se due o più record descrivono la stessa condizione di avviso, gli sqlSTATE di avviso definiti dalla specifica Open Group CLI superano le SQLSTATE definite da ODBC e definite dal driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di più campi di una struttura di dati di diagnosticaObtaining multiple fields of a diagnostic data structure|[Funzione SQLGetDiagRec](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
