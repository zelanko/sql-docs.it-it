---
title: 'Funzione SQLReadFileDSN : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303952"
---
# <a name="sqlreadfiledsn-function"></a>Funzione SQLReadFileDSN
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLReadFileDSN** legge le informazioni da un DSN su file.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszNomefileName (nome file)*  
 [Ingresso] Puntatore al buffer di dati contenente il nome del file DSN. Un'estensione dsn viene aggiunta a tutti i nomi di file che non hanno già un'estensione dsn. Il valore in * \*lpszFileName* deve essere una stringa con terminazione null.  
  
 *NomeAppz*  
 [Ingresso] Puntatore al buffer di dati contenente il nome dell'applicazione. Si tratta di "ODBC" per la sezione ODBC. Il valore in * \*lpszAppName* deve essere una stringa con terminazione null.  
  
 *lpszKeyName (nome di chiave di lavoro)*  
 [Ingresso] Puntatore al buffer di dati contenente il nome della chiave da leggere. Vedere "Commenti" per le parole chiave riservate. Il valore in * \*lpszAppName* deve essere una stringa con terminazione null.  
  
 *lpszString (stringhe)*  
 [Uscita] Puntatore al buffer di dati contenente la stringa associata alla chiave da leggere.  
  
 Se * \*lpszFileName* è un nome di file dsn valido ma *l'argomento lpszAppName* è un puntatore null e l'argomento *lpszKeyName* è un puntatore null, * \*lpszString* contiene un elenco di applicazioni valide. Se * \*lpszFileName* è un nome di file dsn valido e * \*lpszAppName* è un nome di applicazione valido, ma l'argomento *lpszKeyName* è un puntatore null, * \*lpszString* contiene un elenco di parole chiave riservate valide nella sezione appropriata del file DSN, delimitate da punti e virgola. Se * \*lpszFileName* è un nome di file dsn valido ma * \*lpszAppName* è un puntatore null e *l'argomento lpszKeyName* è un puntatore null, * \*lpszString* contiene un elenco delle sezioni nel file DSN, delimitate da punti e virgola.  
  
 *CbStringa*  
 [Ingresso] Lunghezza del * \*buffer lpszString.*  
  
 *stringa pcbString*  
 [Uscita] Numero totale di byte disponibili da restituire in * \*lpszString*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbString*, la stringa di output in * \*lpszString* viene troncata a *cbString* meno il carattere di terminazione null. L'argomento *pcbString* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLReadFileDSN** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszString* era NULL.<br /><br /> L'argomento *cbString* è minore o uguale a 0.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non valido|Il percorso del nome file specificato nell'argomento *lpszFileName* non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *lpszAppName* era NULL, mentre l'argomento *lpszKeyName* era valido.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Stringa di output troncata|La stringa restituita in * \*lpszString* è stata troncata perché il valore in *cbString* è minore o uguale al valore in * \*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non riuscita|La parola chiave non esisteva nel DSN del file.|  
  
## <a name="comments"></a>Commenti  
 ODBC riserva il nome di sezione [ODBC] in cui archiviare le informazioni di connessione. Le parole chiave riservate per questa sezione sono le stesse riservate per una stringa di connessione in **SQLDriverConnect**. (Per altre informazioni, vedere la descrizione della funzione [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Le applicazioni possono utilizzare queste parole chiave riservate per leggere le informazioni in un DSN su file. Se un'applicazione desidera individuare la stringa di connessione senza DSN associata a un DSN su file, è possibile chiamare **SQLReadFileDSN** per una qualsiasi delle parole chiave della stringa di connessione riservata nella sezione [ODBC]. La stringa di connessione completa passata in una connessione senza DSN è una combinazione di tutte le parole chiave (riservate e specifiche del driver) nella sezione [ODBC].  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Scrittura di informazioni in un DSN su file|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
