---
title: SQLWriteFileDSN Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73092fcd7091665f9a3dae969b7821cbf9777c9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63284450"
---
# <a name="sqlwritefiledsn-function"></a>Funzione SQLWriteFileDSN
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLWriteFileDSN** scrive le informazioni in un DSN su File.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszFileName*  
 [Input] Puntatore al nome del DSN su File. Un'estensione DSN viene aggiunto a tutti i nomi di file che non dispongono già di un'estensione DSN.  
  
 *lpszAppName*  
 [Input] Puntatore al nome dell'applicazione. Questo è "ODBC" per la sezione ODBC.  
  
 *lpszKeyName*  
 [Input] Puntatore al nome della chiave da leggere. Per le parole chiave riservate, vedere "Commenti".  
  
 *lpszString*  
 [Output] A cui la stringa associata alla chiave da scrivere. La lunghezza massima della stringa a cui fa riferimento in questo argomento è 32.767 byte.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLWriteFileDSN** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non è valido|Il percorso del nome file specificato nella *lpszFileName* argomento non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *lpszAppName*, *lpszKeyName*, o *lpszString* argomento era NULL.|  
  
## <a name="comments"></a>Commenti  
 ODBC si riserva il nome della sezione [ODBC] in cui archiviare le informazioni di connessione. Le parole chiave riservate di questa sezione corrispondono a quelli riservati per una stringa di connessione in **SQLDriverConnect**. (Per altre informazioni, vedere la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.)  
  
 Le applicazioni possono usare queste parole chiave riservate per scrivere informazioni direttamente in un DSN su File. Se un'applicazione deve creare o modificare la stringa di connessione senza DSN associata a un DSN su File, può chiamare **SQLWriteFileDSN** per una delle parole chiave della stringa di connessione riservate nella sezione [ODBC].  
  
 Se il *lpszString* l'argomento è un puntatore null, la parola chiave a cui punta il *lpszKeyName* argomento verrà eliminato dal file DSN. Se il *lpszString* e *lpszKeyName* argomenti sono entrambi puntatori null, la sezione a cui punta il *lpszAppName* argomento verrà eliminato dal file DSN.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|La lettura delle informazioni di DSN su File|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
