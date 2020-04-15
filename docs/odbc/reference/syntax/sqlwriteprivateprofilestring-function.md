---
title: SqlWritePrivateProfileString (funzione) . Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286884"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Funzione SQLWritePrivateProfileString
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLWritePrivateProfileString** scrive un nome di valore e dati nella sottochiave Odbc.ini delle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszSezione*  
 [Ingresso] Punta a una stringa con terminazione null contenente il nome della sezione in cui verrà copiata la stringa. Se la sezione non esiste, viene creata. Il nome della sezione è indipendente dal caso; la stringa può essere qualsiasi combinazione di lettere maiuscole e minuscole.  
  
 *LpszEntry (ingresso )*  
 [Ingresso] Punta a una stringa con terminazione null contenente il nome della chiave da associare a una stringa. Se la chiave non esiste nella sezione specificata, viene creata. Se questo argomento è NULL, viene eliminata l'intera sezione, incluse tutte le voci all'interno della sezione.  
  
 *lpszString (stringhe)*  
 [Ingresso] Punta a una stringa con terminazione null da scrivere nel file. Se questo argomento è NULL, la chiave a cui fa riferimento l'argomento *lpszEntry* viene eliminata.  
  
 *LpszNome utente*  
 [Uscita] Punta a una stringa con terminazione null che denomina il file di inizializzazione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLWritePrivateProfileString** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non riuscita|Impossibile scrivere le informazioni di sistema richieste.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLWritePrivateProfileString** viene fornito come un modo semplice per convertire i driver e le DLL di installazione dei driver da Microsoft® Windows® a Microsoft Windows NT®/Windows 2000. Le chiamate a **WritePrivateProfileString** che scrivono una stringa di profilo nel file Odbc.ini devono essere sostituite con chiamate a **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** chiama le funzioni nell'API Win32® per aggiungere il nome del valore e i dati specificati alla sottochiave Odbc.ini delle informazioni di sistema.  
  
 Una modalità di configurazione indica dove si trova la voce Odbc.ini in cui si trovano i valori DSN. Se il DSN è un DSN utente (la variabile di stato è USERDSN_ONLY), la funzione scrive nella voce Odbc.ini in HKEY_CURRENT_USER. Se il DSN è un DSN di sistema (SYSTEMDSN_ONLY), la funzione scrive nella voce Odbc.ini in HKEY_LOCAL_MACHINE. Se la variabile di stato è BOTHDSN, HKEY_CURRENT_USER viene provata e, in caso di esito negativo, viene utilizzato HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Ottenere un valore dalle informazioni di sistema|[OGGETTO SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
