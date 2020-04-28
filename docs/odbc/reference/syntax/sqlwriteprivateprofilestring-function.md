---
title: Funzione SQLWritePrivateProfileString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286884"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Funzione SQLWritePrivateProfileString
**Conformità**  
 Versione introdotta: ODBC 2,0  
  
 **Riepilogo**  
 **SQLWritePrivateProfileString** scrive i dati e il nome di un valore nella sottochiave ODBC. ini delle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszSection*  
 Input Punta a una stringa con terminazione null contenente il nome della sezione in cui verrà copiata la stringa. Se la sezione non esiste, viene creata. Il nome della sezione è indipendente dalla distinzione tra maiuscole e minuscole. la stringa può essere costituita da qualsiasi combinazione di lettere maiuscole e minuscole.  
  
 *lpszEntry*  
 Input Punta a una stringa con terminazione null che contiene il nome della chiave da associare a una stringa. Se la chiave non esiste nella sezione specificata, viene creata. Se questo argomento è NULL, viene eliminata l'intera sezione, incluse tutte le voci all'interno della sezione.  
  
 *lpszString*  
 Input Punta a una stringa con terminazione null da scrivere nel file. Se questo argomento è NULL, la chiave a cui fa riferimento l'argomento *lpszEntry* viene eliminata.  
  
 *lpszFilename*  
 Output Punta a una stringa con terminazione null che denomina il file di inizializzazione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLWritePrivateProfileString** restituisce false, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. La tabella seguente elenca i * \*valori pfErrorCode* che possono essere restituiti da **SQLInstallerError** e ne illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non è stato specificato alcun errore di programma di installazione.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non riuscita|Impossibile scrivere le informazioni di sistema richieste.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa di memoria insufficiente.|  
  
## <a name="comments"></a>Commenti  
 **SQLWritePrivateProfileString** viene fornito come metodo semplice per trasferire i driver e le DLL di installazione dei driver da Microsoft® Windows® a Microsoft windows NT®/Windows 2000. Le chiamate a **WritePrivateProfileString** che scrivono una stringa del profilo nel file ODBC. ini devono essere sostituite con chiamate a **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chiama funzioni nell'API Win32® per aggiungere il nome e i dati specificati alla sottochiave ODBC. ini delle informazioni di sistema.  
  
 Una modalità di configurazione indica il punto in cui la voce ODBC. ini che elenca i valori DSN è presente nelle informazioni sul sistema. Se il DSN è un DSN utente (la variabile di stato è USERDSN_ONLY), la funzione scrive nella voce ODBC. ini nel HKEY_CURRENT_USER. Se il DSN è un DSN di sistema (SYSTEMDSN_ONLY), la funzione scrive nella voce ODBC. ini nel HKEY_LOCAL_MACHINE. Se la variabile di stato è BOTHDSN, viene tentata HKEY_CURRENT_USER e, in caso di errore, viene utilizzato HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Ottenere un valore dalle informazioni di sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
