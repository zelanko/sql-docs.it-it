---
title: Funzione SQLInstallerError . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302102"
---
# <a name="sqlinstallererror-function"></a>Funzione SQLInstallerError
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallerError** restituisce informazioni sull'errore o sullo stato per le funzioni del programma di installazione ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *errore iError*  
 [Ingresso] Numero di record di errore. I numeri validi sono compresi tra 1 e 8.  
  
 *pfErrorCode (codice pfErrorCode)*  
 [Uscita] Codice di errore del programma di installazione. (Per ulteriori informazioni, vedere "Commenti".  
  
 *lpszErrorMsg*  
 [Uscita] Puntatore all'archiviazione per il testo del messaggio di errore.  
  
 *CbErrorMsgMax*  
 [Ingresso] Lunghezza massima del buffer *szErrorMsg.* Deve essere minore o uguale a SQL_MAX_MESSAGE_LENGTH meno il carattere di terminazione null.  
  
 *CbErrorMsgMax*  
 [Ingresso] Lunghezza massima del buffer *szErrorMsg.* Deve essere minore o uguale a SQL_MAX_MESSAGE_LENGTH meno il carattere di terminazione null.  
  
 *pcbErrorMsg (informazioni in due)*  
 [Uscita] Puntatore al numero totale di byte (escluso il carattere di terminazione null) disponibile per la restituzione in *lpszErrorMsg*. Se il numero di byte disponibili per la restituzione è maggiore o uguale a *cbErrorMsgMax*, il testo del messaggio di errore in *lpszErrorMsg* viene troncato a *cbErrorMsgMax* meno i byte di caratteri di terminazione null. L'argomento *pcbErrorMsg* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLInstallerError** non registra i valori di errore per se stesso. **SQLInstallerError** restituisce SQL_NO_DATA quando non è in grado di recuperare informazioni sull'errore (nel qual caso *pfErrorCode* è indefinito). Se **SQLInstallerError** non è in grado di accedere ai valori di errore per qualsiasi motivo che normalmente restituisce SQL_ERROR, **SQLInstallerError** restituisce SQL_ERROR ma non registra alcun valore di errore. Se non si conosce la lunghezza della stringa di avviso (*lpszErrorMsg*), è possibile impostare *lpszErrorMsg* su NULL e chiamare **SQLInstallerError**. **SQLInstallerError** restituirà quindi la lunghezza della stringa di avviso in *cbErrorMsgMax*. Se il buffer per il messaggio di errore è troppo breve, **SQLInstallerError** restituisce SQL_SUCCESS_WITH_INFO e restituisce il valore *pfErrorCode* corretto per **SQLInstallerError**.  
  
 Per determinare se si è verificato un troncamento nel messaggio di errore, un'applicazione può confrontare il valore nell'argomento *cbErrorMsgMax* con la lunghezza effettiva del testo del messaggio scritto nell'argomento *pcbErrorMsg* . Se si verifica il troncamento, la lunghezza del buffer corretta deve essere allocata per *lpszErrorMsg* e **SQLInstallerError** deve essere chiamato nuovamente con il record *iError* corrispondente.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama **SQLInstallerError** quando una chiamata precedente alla funzione del programma di installazione ODBC restituisce FALSE. Il programma di installazione ODBC e le funzioni di installazione del driver o del traduttore registrano zero o più errori solo quando la funzione ha esito negativo (restituisce FALSE); pertanto, un'applicazione chiama **SQLInstallerError** solo dopo che una funzione del programma di installazione ODBC ha esito negativo.  
  
 La coda degli errori del programma di installazione ODBC viene scaricata ogni volta che viene chiamata una nuova funzione del programma di installazione. Pertanto, un'applicazione non può prevedere di recuperare gli errori per le funzioni diverse dall'ultima chiamata di funzione del programma di installazione.  
  
 Per recuperare più errori per una chiamata di funzione, un'applicazione chiama **SQLInstallerError** più volte.  
  
 Quando non sono presenti informazioni aggiuntive, **SQLInstallerError** restituisce SQL_NO_DATA, l'argomento *pfErrorCode* non è definito, l'argomento *pcbErrorMsg* è uguale a 0 e *l'argomento lpszErrorMsg* contiene un singolo carattere di terminazione null (a meno che l'argomento *cbErrorMsgMax non* sia uguale a 0).
