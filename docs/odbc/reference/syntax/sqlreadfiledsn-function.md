---
title: Funzione SQLReadFileDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a247b9916bd4b8bfe8704d7f374ef027043e2ae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262446"
---
# <a name="sqlreadfiledsn-function"></a>Funzione SQLReadFileDSN
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLReadFileDSN** legge le informazioni da un DSN su File.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszFileName*  
 [Input] Puntatore al buffer di dati che contiene il nome del file DSN. Un'estensione di DSN viene aggiunto a tutti i nomi di file che non dispongono già di un'estensione di DSN. Il valore in  *\*lpszFileName* deve essere una stringa con terminazione null.  
  
 *lpszAppName*  
 [Input] Puntatore al buffer di dati che contiene il nome dell'applicazione. Questo è "ODBC" per la sezione ODBC. Il valore in  *\*lpszAppName* deve essere una stringa con terminazione null.  
  
 *lpszKeyName*  
 [Input] Puntatore al buffer di dati che contiene il nome della chiave da leggere. Per le parole chiave riservate, vedere "Commenti". Il valore in  *\*lpszAppName* deve essere una stringa con terminazione null.  
  
 *lpszString*  
 [Output] Puntatore al buffer di dati che contiene la stringa associata alla chiave da leggere.  
  
 Se  *\*lpszFileName* è un nome di file DSN valido, ma il *lpszAppName* argomento è un puntatore null e la *lpszKeyName* argomento è un puntatore null, quindi  *\*lpszString* contiene un elenco di applicazioni valide. Se  *\*lpszFileName* è un nome di file DSN valido e  *\*lpszAppName* è un nome di applicazione valido, ma il *lpszKeyName* argomento è un valore null puntatore, quindi  *\*lpszString* contiene un elenco di parole chiave riservate valide nella sezione appropriata del file DSN, delimitata da punti e virgola. Se  *\*lpszFileName* è un nome di file DSN valido ma  *\*lpszAppName* è un puntatore null e il *lpszKeyName* argomento è un puntatore null, quindi  *\*lpszString* contiene un elenco delle sezioni nel file DSN, delimitate da punti e virgola.  
  
 *cbString*  
 [Input] Lunghezza del  *\*lpszString* buffer.  
  
 *pcbString*  
 [Output] Numero totale di byte disponibili per restituire  *\*lpszString*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbString*, la stringa di output in  *\*lpszString* verranno troncati alla *cbString* meno il carattere di terminazione null. Il *pcbString* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLReadFileDSN** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszString* argomento era NULL.<br /><br /> Il *cbString* argomento era minore o uguale a 0.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non è valido|Il percorso del nome file specificato nella *lpszFileName* argomento non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *lpszAppName* l'argomento è NULL, mentre le *lpszKeyName* argomento è valido.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Stringa di output troncato|La stringa restituita nel  *\*lpszString* è stato troncato perché il valore nella *cbString* era minore o uguale al valore nella  *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non è riuscita|La parola chiave non esiste nel file DSN.|  
  
## <a name="comments"></a>Commenti  
 ODBC si riserva il nome della sezione [ODBC] in cui archiviare le informazioni di connessione. Le parole chiave riservate di questa sezione corrispondono a quelli riservati per una stringa di connessione in **SQLDriverConnect**. (Per altre informazioni, vedere la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.)  
  
 Le applicazioni possono usare queste parole chiave riservate per leggere le informazioni contenute in un DSN su File. Se un'applicazione deve trovare la stringa di connessione senza DSN associata a un DSN su File, può chiamare **SQLReadFileDSN** per una delle parole chiave della stringa di connessione riservate nella sezione [ODBC]. La stringa di connessione completa passata in una connessione senza DSN è una combinazione di tutte le parole chiave (riservate e specifici del driver) nella sezione [ODBC].  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|La scrittura di informazioni in un DSN su File|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
