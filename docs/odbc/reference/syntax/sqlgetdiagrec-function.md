---
title: Funzione SQLGetDiagRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c404cbb1f29adbdcb49ef6bed8bb57a047f64f3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911324"
---
# <a name="sqlgetdiagrec-function"></a>Funzione SQLGetDiagRec
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLGetDiagRec** restituisce i valori correnti di più campi di un record di diagnostica che contiene informazioni sull'errore, avviso e stato. A differenza **SQLGetDiagField**, che restituisce un campo di diagnostica per ogni chiamata **SQLGetDiagRec** restituisce diversi campi di un record di diagnostica, tra cui il valore SQLSTATE, il codice di errore nativo di uso comune e il testo del messaggio di diagnostica.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
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
 [Input] Indica se il record di stato da cui l'applicazione cerca le informazioni. Record di stato vengono numerati da 1.  
  
 *SQLState*  
 [Output] Puntatore a un buffer in cui si desidera restituire un codice di errore SQLSTATE di cinque caratteri (e carattere di terminazione NULL) per il record di diagnostica *RecNumber*. I primi due caratteri indicano alla classe. i successivi tre indicano la sottoclasse. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_SQLSTATE. Per altre informazioni, vedere [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Output] Puntatore a un buffer in cui restituire il codice di errore nativo specifico per l'origine dati. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Output] Puntatore a un buffer in cui restituire la stringa di testo del messaggio di diagnostica. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_MESSAGE_TEXT. Per il formato della stringa, vedere [messaggi diagnostici](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *MessageText* sia impostato su NULL *TextLengthPtr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *MessageText*.  
  
 *BufferLength*  
 [Input] Lunghezza di **MessageText* buffer in caratteri. È prevista una lunghezza massima del testo del messaggio di diagnostica.  
  
 *TextLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il numero di caratteri necessari per il carattere di terminazione null) disponibili per restituire  *\*MessageText*. Se il numero di caratteri disponibili da restituire è maggiore *BufferLength*, il testo del messaggio di diagnostica nel  *\*MessageText* viene troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLGetDiagRec** non invia i record di diagnostica per se stesso. Usa i seguenti valori restituiti per segnalare il risultato della propria esecuzione:  
  
-   SQL_SUCCESS: La funzione viene restituito correttamente le informazioni di diagnostica.  
  
-   SQL_SUCCESS_WITH_INFO: Il \* *MessageText* buffer è troppo piccolo per contenere il messaggio di diagnostica richiesto. Nessun record di diagnostica sono stati generati. Per determinare che si è verificato un troncamento, l'applicazione deve confrontare *BufferLength* al numero effettivo di byte disponibili, che viene scritto in **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: L'handle indicato dal *HandleType* e *gestire* non era un handle valido.  
  
-   SQL_ERROR: Si è verificata una delle operazioni seguenti:  
  
    -   *RecNumber* è negativo o 0.  
  
    -   *BufferLength* era minore di zero.  
  
    -   Quando si utilizza la notifica asincrona, l'operazione asincrona sull'handle non è completa.  
  
-   SQL_NO_DATA: *RecNumber* era maggiore del numero di record di diagnostica esistenti per l'handle specificato in *gestire.* La funzione restituisce SQL_NO_DATA anche per qualsiasi positivo *RecNumber* se non sono presenti record di diagnostica per *gestire*.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere **SQLGetDiagRec** quando una precedente chiamata a una funzione ODBC ha restituito SQL_ERROR o SQL_SUCCESS_WITH_INFO. Tuttavia, poiché una funzione ODBC possa registrare i record di diagnostica di zero o più ogni volta che viene chiamato, un'applicazione può chiamare **SQLGetDiagRec** dopo una chiamata di funzione ODBC. Un'applicazione può chiamare **SQLGetDiagRec** più volte per restituire alcuni o tutti i record nella struttura di dati di diagnostica. ODBC non impone alcun limite al numero di record di diagnostica che possono essere archiviati in qualsiasi momento.  
  
 **SQLGetDiagRec** non può essere utilizzata per restituire i campi dall'intestazione della struttura di dati di diagnostica. (Il *RecNumber* argomento deve essere maggiore di 0.) L'applicazione deve chiamare **SQLGetDiagField** per questo scopo.  
  
 **SQLGetDiagRec** recupera solo le informazioni di diagnostica più recente associate al punto specificato nella *gestire* argomento. Se l'applicazione chiama un'altra funzione ODBC, eccetto **SQLGetDiagRec**, **SQLGetDiagField**, o **SQLError**, le informazioni di diagnostica dalle chiamate precedenti di stesso handle è perso.  
  
 Un'applicazione può analizzare tutti i record di diagnostica dal ciclo, incremento *RecNumber*, purché **SQLGetDiagRec** restituisce SQL_SUCCESS. Le chiamate a **SQLGetDiagRec** siano non distruttive ai campi di intestazione e un record. L'applicazione può chiamare **SQLGetDiagRec** nuovamente in un secondo momento per recuperare un campo da un record, purché in quanto non altra funzione, ad eccezione **SQLGetDiagRec**, **SQLGetDiagField**, oppure **SQLError**, è stato chiamato nel frattempo. L'applicazione può anche recuperare un conteggio del numero totale di record di diagnostica disponibile chiamando **SQLGetDiagField** per recuperare il valore del campo SQL_DIAG_NUMBER e quindi chiamando **SQLGetDiagRec**numero di volte indicato.  
  
 Per una descrizione dei campi della struttura di dati di diagnostica, vedere [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Per altre informazioni, vedere [utilizzo di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [implementazione di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chiama un'API diverso da quello che viene eseguita in modo asincrono genererà HY010 "Errore nella sequenza della funzione". Tuttavia, il record di errore non è possibile recuperare prima del completamento dell'operazione asincrona.  
  
## <a name="handletype-argument"></a>Argomento HandleType  
 Ogni tipo di handle può avere informazioni di diagnostica associate. Il *HandleType* argomento indica il tipo di handle delle *gestire* argomento.  
  
 Alcuni campi di intestazione e record non possono essere restituiti per l'ambiente, connessione, istruzione e descrittore handle. Tali handle per il quale non è applicabile un campo sono indicati nelle sezioni "Campi di Record" e "Campi di intestazione" nella [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Una chiamata a **SQLGetDiagRec** verrà restituito SQL_INVALID_HANDLE se *HandleType* è SQL_HANDLE_SENV, che indica un handle di ambiente condiviso. Tuttavia, se *HandleType* SQL_HANDLE_ENV, viene *gestire* può essere condivisa o un handle di ambiente non condiviso.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di un campo di un record di diagnostica o un campo dell'intestazione di diagnostica|[Funzione SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md)
