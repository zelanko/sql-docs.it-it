---
title: Funzione SQLInstallerError | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d5e05e62350d916e9c5fcf680af05717b39aa58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242331"
---
# <a name="sqlinstallererror-function"></a>Funzione SQLInstallerError
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallerError** restituisce le informazioni di stato o di errore per le funzioni del programma di installazione ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *iError*  
 [Input] Numero di record di errore. Numeri validi sono da 1 a 8.  
  
 *pfErrorCode*  
 [Output] Codice di errore di programma di installazione. (Per altre informazioni, vedere "Commenti".)  
  
 *lpszErrorMsg*  
 [Output] Puntatore alla risorsa di archiviazione per il testo del messaggio di errore.  
  
 *cbErrorMsgMax*  
 [Input] Lunghezza massima del *szErrorMsg* buffer. Deve essere minore o uguale a SQL_MAX_MESSAGE_LENGTH meno il carattere di terminazione null.  
  
 *cbErrorMsgMax*  
 [Input] Lunghezza massima del *szErrorMsg* buffer. Deve essere minore o uguale a SQL_MAX_MESSAGE_LENGTH meno il carattere di terminazione null.  
  
 *pcbErrorMsg*  
 [Output] Puntatore al numero totale di byte (escluso il carattere di terminazione null) disponibili per restituire *lpszErrorMsg*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbErrorMsgMax*, il testo del messaggio di errore in *lpszErrorMsg* verrà troncato *cbErrorMsgMax* meno di byte di caratteri di terminazione null. Il *pcbErrorMsg* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLInstallerError** non registra i valori di errore per se stesso. **SQLInstallerError** restituisce SQL_NO_DATA quando non è in grado di recuperare le informazioni sugli errori (nel qual caso *pfErrorCode* è definito). Se **SQLInstallerError** non è possibile accedere ai valori di errore per qualsiasi motivo che normalmente restituisce SQL_ERROR, **SQLInstallerError** restituisce SQL_ERROR ma non invia i valori di errore. Se non si conosce la lunghezza della stringa di avviso (*lpszErrorMsg*), è possibile impostare *lpszErrorMsg* NULL e chiamare **SQLInstallerError**. **SQLInstallerError** restituirà quindi la lunghezza della stringa di avviso in *cbErrorMsgMax*. Se il buffer per il messaggio di errore è troppo corto **SQLInstallerError** restituisce SQL_SUCCESS_WITH_INFO e restituisce il valore corretto *pfErrorCode* value per **SQLInstallerError**.  
  
 Per determinare se il troncamento si è verificato nel messaggio di errore, un'applicazione in grado di confrontare il valore nel *cbErrorMsgMax* argomento per la lunghezza effettiva del testo del messaggio scritto le *pcbErrorMsg* argomento. Se il troncamento si verifica, la lunghezza del buffer corrette allocare *lpszErrorMsg* e **SQLInstallerError** deve essere chiamato nuovamente con i corrispondenti *iError*record.  
  
## <a name="comments"></a>Commenti  
 Un'applicazione chiama **SQLInstallerError** quando una precedente chiamata alla funzione di programma di installazione ODBC restituisce FALSE. Funzioni di installazione di programma di installazione e driver o funzione di conversione ODBC segnalato zero o più errori solo quando la funzione ha esito negativo, restituisce FALSE, Pertanto, un'applicazione chiama **SQLInstallerError** solo dopo l'esito negativo di una funzione di programma di installazione ODBC.  
  
 Nella coda degli errori di programma di installazione ODBC verrà scaricata ogni volta che viene chiamata una nuova funzione di programma di installazione. Pertanto, un'applicazione non può prevedere di recuperare gli errori di funzioni diverso dall'ultima chiamata di funzione di programma di installazione.  
  
 Per recuperare gli errori più di una chiamata di funzione, un'applicazione chiama **SQLInstallerError** più volte.  
  
 Quando non sono disponibili informazioni aggiuntive, **SQLInstallerError** restituisca SQL_NO_DATA, il *pfErrorCode* argomento non è definito, il *pcbErrorMsg* argomento è uguale a 0, e il *lpszErrorMsg* l'argomento contiene un singolo carattere di terminazione null (a meno che non le *cbErrorMsgMax* argomento è uguale a 0).
