---
title: 'Funzione SQLWriteFileDSN : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286891"
---
# <a name="sqlwritefiledsn-function"></a>Funzione SQLWriteFileDSN
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLWriteFileDSN** scrive informazioni in un DSN su file.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszNomefileName (nome file)*  
 [Ingresso] Puntatore al nome del DSN su file. Un'estensione DSN viene aggiunta a tutti i nomi di file che non hanno già un'estensione DSN.  
  
 *NomeAppz*  
 [Ingresso] Puntatore al nome dell'applicazione. Si tratta di "ODBC" per la sezione ODBC.  
  
 *lpszKeyName (nome di chiave di lavoro)*  
 [Ingresso] Puntatore al nome della chiave da leggere. Vedere "Commenti" per le parole chiave riservate.  
  
 *lpszString (stringhe)*  
 [Uscita] Punta alla stringa associata alla chiave da scrivere. La lunghezza massima della stringa a cui fa riferimento questo argomento è 32.767 byte.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLWriteFileDSN** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non valido|Il percorso del nome file specificato nell'argomento *lpszFileName* non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *lpszAppName*, *lpszKeyName*o *lpszString* era NULL.|  
  
## <a name="comments"></a>Commenti  
 ODBC riserva il nome di sezione [ODBC] in cui archiviare le informazioni di connessione. Le parole chiave riservate per questa sezione sono le stesse riservate per una stringa di connessione in **SQLDriverConnect**. (Per altre informazioni, vedere la descrizione della funzione [SQLDriverConnect.)](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
 Le applicazioni possono utilizzare queste parole chiave riservate per scrivere informazioni direttamente in un DSN su file. Se un'applicazione desidera creare o modificare la stringa di connessione senza DSN associata a un DSN su file, può chiamare **SQLWriteFileDSN** per una qualsiasi delle parole chiave della stringa di connessione riservate nella sezione [ODBC].  
  
 Se l'argomento *lpszString* è un puntatore null, la parola chiave a cui fa riferimento l'argomento *lpszKeyName* verrà eliminata dal file DSN. Se gli argomenti *lpszString* e *lpszKeyName* sono entrambi puntatori null, la sezione a cui fa riferimento l'argomento *lpszAppName* verrà eliminata dal file DSN.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Lettura di informazioni da DSN su file|[SQLReadFileDSN (Informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
