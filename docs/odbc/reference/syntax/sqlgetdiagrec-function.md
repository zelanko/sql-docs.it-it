---
title: SqlGetDiagRec (funzione) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285381"
---
# <a name="sqlgetdiagrec-function"></a>Funzione SQLGetDiagRec
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetDiagRec** restituisce i valori correnti di più campi di un record di diagnostica che contiene informazioni su errori, avvisi e stato. A differenza **di SQLGetDiagField**, che restituisce un campo di diagnostica per ogni chiamata, **SQLGetDiagRec** restituisce diversi campi di uso comune di un record di diagnostica, tra cui SQLSTATE, il codice di errore nativo e il testo del messaggio di diagnostica.  
  
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
 [Ingresso] Indica il record di stato da cui l'applicazione cerca informazioni. I record di stato sono numerati a partire da 1.  
  
 *Sqlstate*  
 [Uscita] Puntatore a un buffer in cui restituire un codice SQLSTATE di cinque caratteri (e terminando NULL) per il record di diagnostica *RecNumber*. I primi due caratteri indicano la classe; i tre successivi indicano la sottoclasse. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_SQLSTATE. Per ulteriori informazioni, vedere [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il codice di errore nativo, specifico dell'origine dati. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Uscita] Puntatore a un buffer in cui restituire la stringa di testo del messaggio di diagnostica. Queste informazioni sono contenute nel campo di diagnostica SQL_DIAG_MESSAGE_TEXT. Per il formato della stringa, vedere [Messaggi di diagnostica](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *MessageText* è NULL, *TextLengthPtr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *MessageText*.  
  
 *BufferLength*  
 [Ingresso] Lunghezza del buffer*MessageText* in caratteri. Non esiste una lunghezza massima del testo del messaggio di diagnostica.  
  
 *TextLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il numero di caratteri necessari per il carattere di terminazione null) disponibile per la restituzione in * \*MessageText*. Se il numero di caratteri disponibili per la restituzione è maggiore di *BufferLength*, il testo del messaggio di diagnostica in * \*MessageText* viene troncato a *BufferLength* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLGetDiagRec** non registra record di diagnostica per se stesso. Utilizza i seguenti valori restituiti per segnalare il risultato della propria esecuzione:  
  
-   SQL_SUCCESS: la funzione ha restituito correttamente le informazioni di diagnostica.  
  
-   SQL_SUCCESS_WITH_INFO: \*il buffer *MessageText* era troppo piccolo per contenere il messaggio di diagnostica richiesto. Non sono stati generati record di diagnostica. Per determinare che si è verificato un troncamento, l'applicazione deve confrontare *BufferLength* con il numero effettivo di byte disponibili, che viene scritto in*StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: l'handle indicato da *HandleType* e *Handle* non è un handle valido.  
  
-   SQL_ERROR: si è verificato uno dei seguenti:  
  
    -   *RecNumber* era negativo o 0.  
  
    -   *BufferLength* era minore di zero.  
  
    -   Quando si utilizza la notifica asincrona, l'operazione asincrona sull'handle non è stata completata.  
  
-   SQL_NO_DATA: *RecNumber* era maggiore del numero di record di diagnostica esistenti per l'handle specificato in *Handle.* La funzione restituisce inoltre SQL_NO_DATA per qualsiasi *RecNumber* positivo se non sono presenti record di diagnostica per *Handle*.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama in genere **SQLGetDiagRec** quando una chiamata precedente a una funzione ODBC ha restituito SQL_ERROR o SQL_SUCCESS_WITH_INFO. Tuttavia, poiché qualsiasi funzione ODBC può registrare zero o più record di diagnostica ogni volta che viene chiamata, un'applicazione può chiamare **SQLGetDiagRec** dopo qualsiasi chiamata di funzione ODBC. Un'applicazione può chiamare **SQLGetDiagRec** più volte per restituire alcuni o tutti i record nella struttura dei dati di diagnostica. ODBC non impone alcun limite al numero di record di diagnostica che possono essere archiviati contemporaneamente.  
  
 **Impossibile utilizzare SQLGetDiagRec** per restituire campi dall'intestazione della struttura dei dati di diagnostica. L'argomento *RecNumber* deve essere maggiore di 0. L'applicazione deve chiamare **SQLGetDiagField** per questo scopo.  
  
 **SQLGetDiagRec** recupera solo le informazioni di diagnostica associate più di recente all'handle specificato nel *Handle* argomento. Se l'applicazione chiama un'altra funzione ODBC, ad eccezione **di SQLGetDiagRec**, **SQLGetDiagField**o **SQLError**, tutte le informazioni di diagnostica delle chiamate precedenti sullo stesso handle vengono perse.  
  
 Un'applicazione può eseguire la scansione di tutti i record di diagnostica eseguendo un ciclo, incrementando *RecNumber*, purché **SQLGetDiagRec restituisca** SQL_SUCCESS. Le chiamate a **SQLGetDiagRec** non sono distruttive per i campi di intestazione e record. L'applicazione può chiamare nuovamente **SQLGetDiagRec** in un secondo momento per recuperare un campo da un record, purché nessun'altra funzione, ad eccezione di **SQLGetDiagRec**, **SQLGetDiagField**o **SQLError**, è stata chiamata nel frattempo. L'applicazione può inoltre recuperare un conteggio del numero totale di record di diagnostica disponibili chiamando **SQLGetDiagField** per recuperare il valore del campo SQL_DIAG_NUMBER e quindi chiamando **SQLGetDiagRec** tale volte.  
  
 Per una descrizione dei campi della struttura dei dati di diagnostica, vedere [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Per ulteriori informazioni, vedere [Utilizzo di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e Implementazione di [SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 La chiamata a un'API diversa da quella eseguita in modo asincrono genererà HY010 "Errore di sequenza di funzioni". Tuttavia, il record di errore non può essere recuperato prima del completamento dell'operazione asincrona.  
  
## <a name="handletype-argument"></a>Argomento HandleType  
 A ogni tipo di handle possono essere associate informazioni di diagnostica. L'argomento *HandleType* indica il tipo di handle dell'argomento *Handle.*  
  
 Alcuni campi di intestazione e record non possono essere restituiti per gli handle di ambiente, connessione, istruzione e descrittore. Gli handle per i quali un campo non è applicabile sono indicati nelle sezioni "Campi intestazione" e "Campi record" in [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Una chiamata a **SQLGetDiagRec** restituirà SQL_INVALID_HANDLE se *HandleType* è SQL_HANDLE_SENV, che denota un handle di ambiente condiviso. Tuttavia, se *HandleType* è SQL_HANDLE_ENV, *Handle* può essere un handle di ambiente condiviso o non condiviso.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di un campo di un record di diagnostica o di un campo dell'intestazione diagnostica|[Funzione SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programma di esempio ODBC](../../../odbc/reference/sample-odbc-program.md)
