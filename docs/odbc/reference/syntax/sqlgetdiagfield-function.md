---
title: Funzione SQLGetDiagField | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13ab95c762573be002782c06615fc6f01317499f
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044298"
---
# <a name="sqlgetdiagfield-function"></a>Funzione SQLGetDiagField

**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetDiagField** restituisce il valore corrente di un campo di un record della struttura di dati di diagnostica (associata a un handle specificato) che contiene informazioni sull'errore, avviso e stato.  
  
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
 [Input] Un identificatore di tipo di handle che descrive il tipo di handle per il quale diagnostica è obbligatoria. I possibili valori sono i seguenti:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Handle SQL_HANDLE_DBC_INFO_TOKEN è utilizzato solo da Gestione Driver e del driver. Le applicazioni non devono usare questo tipo di handle. Per altre informazioni sulle SQL_HANDLE_DBC_INFO_TOKEN, vedere [lo sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Input] Un handle per la struttura di dati di diagnostica, del tipo indicato dal *HandleType*. Se *HandleType* SQL_HANDLE_ENV, viene *gestire* può essere condivisa o un handle di ambiente non condiviso.  
  
 *RecNumber*  
 [Input] Indica se il record di stato da cui l'applicazione cerca le informazioni. Record di stato vengono numerati da 1. Se il *DiagIdentifier* l'argomento indica un qualsiasi campo di intestazione di diagnostica *RecNumber* viene ignorato. In caso contrario, deve essere maggiore di 0.  
  
 *DiagIdentifier*  
 [Input] Indica il campo della diagnostica il cui valore deve essere restituita. Per altre informazioni, vedere la "*DiagIdentifier* argomento" sezione "Commenti".  
  
 *DiagInfoPtr*  
 [Output] Puntatore a un buffer in cui si desidera restituire le informazioni di diagnostica. Il tipo di dati dipende dal valore della *DiagIdentifier*. Se *DiagInfoPtr* è di tipo integer, le applicazioni devono utilizzare un buffer di SQLULEN e inizializzare il valore su 0 prima di chiamare questa funzione, come alcuni driver può solo scrivere l'inferiore a 32 bit o 16 bit di un buffer e lasciare l'ordine più elevato bit non viene modificato.  
  
 Se *DiagInfoPtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *DiagInfoPtr*.  
  
 *BufferLength*  
 [Input] Se *DiagIdentifier* è una diagnostica definite da ODBC e *DiagInfoPtr* punta a una stringa di caratteri o un buffer binario, la lunghezza di questo argomento deve essere \* *DiagInfoPtr* . Se *DiagIdentifier* è un campo definite da ODBC e \* *DiagInfoPtr* è un intero *BufferLength* viene ignorato. Se il valore in  *\*DiagInfoPtr* è una stringa Unicode (quando si chiama **SQLGetDiagFieldW**), il *BufferLength* argomento deve essere un numero pari.  
  
 Se *DiagIdentifier* è un campo definito dal driver, l'applicazione indica la natura del campo da Gestione Driver impostando il *BufferLength* argomento. *BufferLength* può avere i valori seguenti:  
  
-   Se *DiagInfoPtr* è un puntatore a una stringa di caratteri *BufferLength* è la lunghezza della stringa o SQL_NTS.  
  
-   Se *DiagInfoPtr* è un puntatore a un buffer binario, le posizioni dell'applicazione il risultato del SQL_LEN_BINARY_ATTR (*lunghezza*) (macro) in *BufferLength*. Un valore negativo in questo modo vengono inserite *BufferLength*.  
  
-   Se *DiagInfoPtr* è un puntatore a un valore diverso da una stringa di caratteri o stringa binaria *BufferLength* deve avere il valore SQL_IS_POINTER.  
  
-   Se  *\*DiagInfoPtr* contiene un tipo di dati a lunghezza fissa *BufferLength* è SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, come appropriato.  
  
 *StringLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il numero di byte necessari per il carattere di terminazione null) disponibili per restituire \* *DiagInfoPtr*, per dati di tipo carattere. Se il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, il testo nella \* *DiagInfoPtr* verranno troncati alla *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLGetDiagField** non invia i record di diagnostica per se stesso. Usa i seguenti valori restituiti per segnalare il risultato della propria esecuzione:  
  
-   SQL_SUCCESS: La funzione viene restituito correttamente le informazioni di diagnostica.  
  
-   SQL_SUCCESS_WITH_INFO: \**DiagInfoPtr* è troppo piccolo per contenere il campo di diagnostica richiesto. Di conseguenza, i dati nel campo di diagnostica sono stati troncati. Per determinare che si è verificato un troncamento, l'applicazione deve confrontare *BufferLength* al numero effettivo di byte disponibili, che viene scritto in **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: L'handle indicato dal *HandleType* e *gestire* non era un handle valido.  
  
-   SQL_ERROR: Si è verificata una delle operazioni seguenti:  
  
    -   *Il DiagIdentifier* argomento non è uno dei valori validi.  
  
    -   *Il DiagIdentifier* argomento era SQL_DIAG_CURSOR_ROW_COUNT, SQL_DIAG_DYNAMIC_FUNCTION, SQL_DIAG_DYNAMIC_FUNCTION_CODE o SQL_DIAG_ROW_COUNT, ma *gestire* non era un handle di istruzione. (Gestione Driver restituisce questa diagnostica).  
  
    -   *Il RecNumber* argomento è negativo o uguale a 0 quando *DiagIdentifier* indicato un campo da un record di diagnostica. *RecNumber* viene ignorato per i campi di intestazione.  
  
    -   Il valore richiesto è una stringa di caratteri e *BufferLength* era minore di zero.  
  
    -   Quando si utilizza la notifica asincrona, l'operazione asincrona sull'handle non è completa.  
  
-   SQL_NO_DATA: *RecNumber* era maggiore del numero di record di diagnostica esistenti per l'handle specificato in *gestire.* La funzione restituisce SQL_NO_DATA anche per qualsiasi positivo *RecNumber* se non sono presenti record di diagnostica per *gestire*.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere **SQLGetDiagField** a completare una delle tre obiettivi:  
  
1.  Per ottenere le informazioni sull'avviso o errore specifico durante una chiamata di funzione ha restituito SQL_ERROR o SQL_SUCCESS_WITH_INFO (o SQL_NEED_DATA per il **SQLBrowseConnect** (funzione)).  
  
2.  Per determinare il numero di righe nell'origine dati che sono state interessate durante le operazioni update, delete o insert eseguite con una chiamata a **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, oppure **SQLSetPos** (tra il campo di intestazione SQL_DIAG_ROW_COUNT), o per determinare il numero di righe presenti nel cursore aperto corrente, se il driver può fornire queste informazioni (dal Campo di intestazione SQL_DIAG_CURSOR_ROW_COUNT).  
  
3.  Per determinare quale funzione è stata eseguita da una chiamata a **SQLExecDirect** oppure **SQLExecute** (dai campi intestazione SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE).  
  
 Una funzione ODBC possa registrare zero o più record di diagnostica ogni volta che viene chiamata, in modo che un'applicazione può chiamare **SQLGetDiagField** dopo una chiamata di funzione ODBC. Non sono previsti limiti al numero di record di diagnostica che possono essere archiviati in qualsiasi momento. **SQLGetDiagField** recupera solo le informazioni di diagnostica associate alla struttura dei dati di diagnostica specificata in più di recente il *gestire* argomento. Se l'applicazione chiama una funzione ODBC diverso da **SQLGetDiagField** oppure **SQLGetDiagRec**, le informazioni di diagnostica da una precedente chiamata con lo stesso handle vengono perse.  
  
 Un'applicazione può analizzare tutti i record di diagnostica incrementando *RecNumber*, purché **SQLGetDiagField** restituisce SQL_SUCCESS. Il numero di record di stato è indicato nel campo dell'intestazione SQL_DIAG_NUMBER. Le chiamate a **SQLGetDiagField** siano non distruttive ai campi di intestazione e un record. L'applicazione può chiamare **SQLGetDiagField** nuovamente in seguito per recuperare un campo da un record, fino a quando una funzione diversa dalle funzionalità di diagnostica non è stata chiamata nel frattempo, che generava i record sullo stesso handle.  
  
 Un'applicazione può chiamare **SQLGetDiagField** da restituire qualsiasi campo di diagnostica in qualsiasi momento, fatta eccezione per SQL_DIAG_CURSOR_ROW_COUNT o SQL_DIAG_ROW_COUNT, che restituisce SQL_ERROR se *gestire* non è un handle di istruzione. Se gli altri campi di diagnostica non sono definito, la chiamata a **SQLGetDiagField** restituisce SQL_SUCCESS (a condizione che non viene rilevata alcun altra diagnostica) e viene restituito un valore indefinito per il campo.  
  
 Per altre informazioni, vedere [utilizzo di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [implementazione di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chiama un'API diverso da quello che viene eseguita in modo asincrono genererà HY010 "Errore nella sequenza della funzione". Tuttavia, il record di errore non è possibile recuperare prima del completamento dell'operazione asincrona.  
  
## <a name="handletype-argument"></a>Argomento HandleType  
 Ogni tipo di handle può avere informazioni di diagnostica associate. Il *HandleType* l'argomento indica il tipo di handle del *gestire*.  
  
 Alcuni campi di intestazione e record non possono essere restituiti per l'ambiente, connessione, istruzione e descrittore handle. Tali handle per il quale non è applicabile un campo sono indicati nelle sezioni "Campi di Record" e "Campi di intestazione" seguente.  
  
 Se *HandleType* SQL_HANDLE_ENV, viene *gestire* può essere un handle di ambiente condiviso o annullata.  
  
 Alcun campo di diagnostica specifici del driver intestazione non deve essere associato a un handle di ambiente.  
  
 I campi di intestazione solo diagnostica definiti per un handle descrittore sono SQL_DIAG_NUMBER e SQL_DIAG_RETURNCODE.  
  
## <a name="diagidentifier-argument"></a>Argomento DiagIdentifier  
 Questo argomento indica l'identificatore del campo richiesto dalla struttura di dati di diagnostica. Se *RecNumber* è maggiore o uguale a 1, i dati nel campo descrivono le informazioni di diagnostica restituite da una funzione. Se *RecNumber* è 0, il campo è contenuto nell'intestazione della struttura di dati di diagnostica e di conseguenza contiene dati relativi alla chiamata di funzione che ha restituito le informazioni di diagnostica, non per le informazioni specifiche.  
  
 I driver possono definire intestazione specifico del driver e i campi di record nella struttura di dati di diagnostica.  
  
 Un'applicazione ODBC 3 *. x* funziona con un'API ODBC 2 *. x* driver sarà in grado di chiamare **SQLGetDiagField** solo con un *DiagIdentifier* argomento di SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Tutti gli altri campi di diagnostica restituirà SQL_ERROR.  
  
## <a name="header-fields"></a>Campi di intestazione  
 I campi di intestazione elencati nella tabella seguente possono essere inclusi nel *DiagIdentifier* argomento.  
  
|DiagIdentifier|Tipo restituito|Valori di codice restituiti|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|Questo campo contiene il conteggio delle righe del cursore. La semantica varia il **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2, SQL_KEYSET_CURSOR_ATTRIBUTES2 e SQL_STATIC_CURSOR_ATTRIBUTES2, che indicano che i tipi di informazioni conteggio delle righe è disponibili per ogni tipo di cursore (in bit SQL_CA2_CRC_EXACT e SQL_CA2_CRC_APPROXIMATE).<br /><br /> Il contenuto di questo campo è definito solo per gli handle di istruzione e solo dopo aver **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato. La chiamata **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_CURSOR_ROW_COUNT in diverso da un'istruzione handle restituirà SQL_ERROR.|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|Si tratta di una stringa che descrive l'istruzione SQL eseguita la funzione sottostante. (Vedere "Valori dei campi, funzione dinamica" più avanti in questa sezione per valori specifici). Il contenuto di questo campo è definito solo per gli handle di istruzione e solo dopo una chiamata a **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults**. La chiamata **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_DYNAMIC_FUNCTION in diverso da un'istruzione handle restituirà SQL_ERROR. Il valore di questo campo non è definito prima della chiamata a **SQLExecute** oppure **SQLExecDirect**.|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|Si tratta di un codice numerico che descrive l'istruzione SQL eseguita dalla funzione sottostante. (Vedere "Valori di the dinamica funzione campi," più avanti in questa sezione per valore specifico.) Il contenuto di questo campo è definito solo per gli handle di istruzione e solo dopo una chiamata a **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults**. La chiamata **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_DYNAMIC_FUNCTION_CODE in diverso da un'istruzione handle restituirà SQL_ERROR. Il valore di questo campo non è definito prima della chiamata a **SQLExecute** oppure **SQLExecDirect**.|  
|SQL_DIAG_NUMBER|SQLINTEGER|Il numero di record di stato che sono disponibili per l'handle specificato.|  
|SQL_DIAG_RETURNCODE|SQLRETURN|Restituire il codice restituito dalla funzione. Per un elenco dei codici restituiti, vedere [codici restituiti](../../../odbc/reference/develop-app/return-codes-odbc.md). Il driver non è necessario implementare SQL_DIAG_RETURNCODE; viene sempre implementato da Gestione Driver. Se nessuna funzione è ancora stata chiamata sul *gestire*, viene restituito SQL_SUCCESS per SQL_DIAG_RETURNCODE.|  
|SQL_DIAG_ROW_COUNT|SQLLEN|Il numero di righe interessate da un inserimento, eliminazione o aggiornamento eseguito dal **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos**. È definito dal driver dopo una *specifica del cursore* è stata eseguita. Il contenuto di questo campo è definito solo per gli handle di istruzione. La chiamata **SQLGetDiagField** con un *DiagIdentifier* di SQL_DIAG_ROW_COUNT in diverso da un'istruzione handle restituirà SQL_ERROR. I dati in questo campo viene inoltre restituiti nel *RowCountPtr* argomenti del **SQLRowCount**. I dati in questo campo viene reimpostati dopo ogni chiamata di funzione nondiagnostic, mentre il numero di righe restituito da **SQLRowCount** rimane invariato fino a quando l'istruzione viene ripristinata allo stato preparato o allocato.|  
  
## <a name="record-fields"></a>Campi di record  
 I campi di record elencati nella tabella seguente possono essere inclusi nel *DiagIdentifier* argomento.  
  
|DiagIdentifier|Tipo restituito|Valori di codice restituiti|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|Stringa che indica il documento che definisce la parte relativa alla classe del valore SQLSTATE di questo record. Il valore è "ISO 9075" per tutti SQLSTATEs definito da Open Group e l'interfaccia a livello di chiamata ISO. Per la specifica ODBC SQLState (tutti quelli la cui classe SQLSTATE è "IM"), il relativo valore è "ODBC 3.0".|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|Se il campo SQL_DIAG_ROW_NUMBER è un numero di riga valido in un set di righe o un set di parametri, questo campo contiene il valore che rappresenta il numero di colonna nel set di risultati o il numero di parametro nel set di parametri. I numeri iniziano sempre da 1; colonna del set di risultati Se questo record di stato si riferisce a una colonna del segnalibro, il campo può essere zero. I numeri di parametro partono da 1. È impostata sul valore SQL_NO_COLUMN_NUMBER se il record di stato non è associato un numero di colonna o numero del parametro. Se il driver non è possibile determinare il numero di colonna o il numero di parametro che è associato questo record, questo campo ha il valore SQL_COLUMN_NUMBER_UNKNOWN.<br /><br /> Il contenuto di questo campo è definito solo per gli handle di istruzione.|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|Stringa che indica il nome della connessione di cui si riferisce al record di diagnostica. Questo campo è definito dal driver. Per le strutture di dati di diagnostica associate all'handle di ambiente e per la diagnostica che non riguardano qualsiasi connessione, questo campo è una stringa di lunghezza zero.|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|Un messaggio informativo in errore o avviso. Questo campo viene formattato come descritto in [messaggi diagnostici](../../../odbc/reference/develop-app/diagnostic-messages.md). È prevista una lunghezza massima per il testo del messaggio di diagnostica.|  
|SQL_DIAG_NATIVE|SQLINTEGER|Un codice di errore nativo specifico dell'origine dati/driver. Se è presente alcun codice di errore nativo, il driver restituisce 0.|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|Questo campo contiene il numero di riga nel set di righe o il numero di parametro nel set di parametri, a cui è associato il record di stato. Numeri di riga e parametro iniziano con 1. Questo campo ha il valore SQL_NO_ROW_NUMBER se questo record di stato non è associato un numero di riga o parametro. Se il driver non è possibile determinare il numero di riga o il numero di parametro che è associato questo record, questo campo ha il valore SQL_ROW_NUMBER_UNKNOWN.<br /><br /> Il contenuto di questo campo è definito solo per gli handle di istruzione.|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|Stringa che indica il nome del server cui si riferisce al record di diagnostica. È uguale al valore restituito per una chiamata a **SQLGetInfo** con l'opzione SQL_DATA_SOURCE_NAME. Per le strutture di dati di diagnostica associate all'handle di ambiente e per la diagnostica non sono correlati a qualsiasi server, questo campo è una stringa di lunghezza zero.|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|Un codice diagnostica SQLSTATE di cinque caratteri. Per altre informazioni, vedere [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|Una stringa con lo stesso formato e i valori validi come SQL_DIAG_CLASS_ORIGIN, che identifica la parte di definizione della parte del codice SQLSTATE sottoclasse. Gli SQLSTATE ODBC specifico per il quale viene restituito "ODBC 3.0" includono quanto segue:<br /><br /> 01S00, 01S01, 01S02, 01S06, 01S07, 07S01, 08S01, 21S01, 21S02, 25S01, 25S02, 25S03, 42S01, 42S02, 42S11, 42S12, 42S21, 42S22, HY095, HY097, HY098, HY099, HY100, HY101, HY105, HY107, HY109, HY110, HY111, HYT00, HYT01, IM001, IM002, IM003, IM004, IM005, IM006, IM007, IM008, IM010, IM011, IM012.|  
  
## <a name="values-of-the-dynamic-function-fields"></a>Valori dei campi di funzione dinamica  
 Nella tabella seguente vengono descritti i valori di SQL_DIAG_DYNAMIC_FUNCTION e SQL_DIAG_DYNAMIC_FUNCTION_CODE che si applicano a ogni tipo di istruzione SQL eseguita da una chiamata a **SQLExecute** o **SQLExecDirect**. Il driver è possibile aggiungere i valori definiti dal driver a quelli elencati.  
  
|Istruzione SQL<br /><br /> eseguito|Valore di<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|Valore di<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-statement*|"ALTER DOMINIO"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-statement*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*assertion-definition*|"CREAZIONE DI ASSERZIONE"|SQL_DIAG_CREATE_ASSERTION|  
|*character-set-definition*|"CREAZIONE DI SET DI CARATTERI"|SQL_DIAG_CREATE_CHARACTER_SET|  
|*collation-definition*|"CREAZIONE DI REGOLE DI CONFRONTO"|SQL_DIAG_CREATE_COLLATION|  
|*domainn-definition*|"CREA DOMINIO"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|"CREA INDICE"|SQL_DIAG_CREATE_INDEX|  
|*create-table-statement*|"CREAZIONE DI TABELLA"|SQL_DIAG_CREATE_TABLE|  
|*create-view-statement*|"CREATE VIEW"|SQL_DIAG_CREATE_VIEW|  
|*cursor-specification*|"SELECT DEL CURSORE"|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-positioned*|"CURSORE DINAMICA DI ELIMINAZIONE"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-statement-searched*|"ELIMINARE WHERE"|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion-statement*|"DROP ASSERZIONE"|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|"IL SET DI CARATTERI DI RILASCIO"|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|"ELENCO DELLE REGOLE DI CONFRONTO"|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|"DROP DOMINIO"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-statement*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-translation-statement*|"DROP TRADUZIONE"|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|PANNELLO "CONCEDI"|SQL_DIAG_GRANT|
|*insert-statement*|"INSERT"|SQL_DIAG_INSERT|  
|*ODBC-procedure-extension*|"CHIAMA"|SQL_DIAG_ CALL|  
|*revoke-statement*|"REVOKE"|SQL_DIAG_REVOKE|  
|*schema-definition*|"CREAZIONE DI SCHEMI"|SQL_DIAG_CREATE_SCHEMA|  
|*translation-definition*|"CREAZIONE DI TRADUZIONE"|SQL_DIAG_CREATE_TRANSLATION|  
|*update-statement-positioned*|"AGGIORNAMENTO DINAMICO CURSOR"|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-searched*|"AGGIORNARE LA POSIZIONE"|SQL_DIAG_UPDATE_WHERE|  
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

 Record di stato vengono posizionati in una sequenza basata sul numero di riga e il tipo della diagnostica. Gestione Driver determina l'ordine finale in cui restituire i record di stato che genera. Il driver determina l'ordine finale in cui restituire i record di stato che genera.  
  
 Se i record di diagnostica vengono inviati da Gestione Driver e il driver, Driver Manager è responsabile ordinandoli.  
  
 Se sono presenti due o più record di stato, la sequenza di record viene determinata innanzitutto dal numero di riga. Per determinare la sequenza di record di diagnostica dalla riga si applicano le regole seguenti:  
  
-   I record che non corrispondono a qualsiasi riga vengono visualizzati prima i record che corrispondono a una determinata riga, perché SQL_NO_ROW_NUMBER viene definito come -1.  
  
-   Vengono visualizzati record per il quale il numero di righe è sconosciuto davanti a tutti gli altri record, poiché SQL_ROW_NUMBER_UNKNOWN viene definito come -2.  
  
-   Per tutti i record relativi a righe specifiche, i record vengono ordinati in base al valore nel campo SQL_DIAG_ROW_NUMBER. Sono elencati tutti gli errori e avvisi della prima riga interessata, e quindi tutti gli errori e avvisi del successivo riga interessata e così via.  
  
> [!NOTE]
>  ODBC 3 *. x* gestione Driver non ordina i record di stato nella coda di diagnostica se SQLSTATE 01S01 (errore nella riga) viene restituito da un'API ODBC 2 *. x* driver o se SQLSTATE 01S01 (errore nella riga) viene restituito da un database ODBC 3 *. x* driver quando **SQLExtendedFetch** viene chiamato oppure **SQLSetPos** viene chiamato su un cursore che è stato posizionato con **SQLExtendedFetch** .  
  
 All'interno di ogni riga, o per tutti i record che non corrispondono a una riga o per i quali il numero di righe è sconosciuto, o per tutti i record con un numero di riga uguale a SQL_NO_ROW_NUMBER, il primo record elencati è determinato dall'utilizzo di un set di regole di ordinamento. Dopo il primo record, l'ordine dei record che interessano una riga è definito. Un'applicazione non può presupporre che gli errori precedono gli avvisi dopo il primo record. Le applicazioni devono essere analizzati la struttura di dati di diagnostica completa per ottenere informazioni complete su una chiamata a una funzione.  
  
 Le regole seguenti vengono utilizzate per determinare il primo record all'interno di una riga. Il record con il valore più alto è il primo record. L'origine di un record (gestione Driver, driver, gateway e così via) non viene considerato quando i record di rango.  
  
-   **Errori** record di stato che descrivono gli errori hanno la priorità più alta. Per ordinare gli errori vengono applicate le regole seguenti:  
  
    -   I record che indicano un errore della transazione o un errore della transazione possibili outrank tutti gli altri record.  
  
    -   Se due o più record di descrivere la stessa condizione di errore, definito dalla specifica Open dell'interfaccia della riga di gruppo (classi 03 tramite HZ) SQLSTATEs outrank SQLSTATE ODBC e driver definiti.  
  
-   **N valori di dati definito dall'implementazione** i record di stato che descrivono i valori di dati non definiti dal driver (classe 02) hanno la seconda priorità più alta.  
  
-   **Avvisi** i record di stato che descrivono gli avvisi (classe 01) hanno la priorità più bassa. Se due o più record di descrivere la stessa condizione di avviso, quindi avviso SQLSTATEs definito dalla specifica CLI di gruppo aprire outrank SQLSTATEs definite da ODBC e definiti dal driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di più campi di una struttura di dati di diagnostica|[Funzione SQLGetDiagRec](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
