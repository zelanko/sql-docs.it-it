---
title: Funzione SQLConfigDataSource . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90a51193a8f4edbb013527c4dde0625b75131583
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299631"
---
# <a name="sqlconfigdatasource-function"></a>Funzione SQLConfigDataSource
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLConfigDataSource** aggiunge, modifica o elimina origini dati.  
  
 È possibile accedere alla funzionalità di **SQLConfigDataSource** anche con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndPadre*  
 [Ingresso] Handle della finestra padre. La funzione non visualizzerà alcuna finestra di dialogo se l'handle è null.  
  
 *fRichiesta*  
 [Ingresso] Tipo di richiesta. L'argomento *fRequest* deve contenere uno dei valori seguenti:  
  
 ODBC_ADD_DSN: aggiungere una nuova origine dati utente.  
  
 ODBC_CONFIG_DSN: configurare (modificare) un'origine dati utente esistente.  
  
 ODBC_REMOVE_DSN: rimuovere un'origine dati utente esistente.  
  
 ODBC_ADD_SYS_DSN: aggiungere una nuova origine dati di sistema.  
  
 ODBC_CONFIG_SYS_DSN: modificare un'origine dati di sistema esistente.  
  
 ODBC_REMOVE_SYS_DSN: rimuovere un'origine dati di sistema esistente.  
  
 ODBC_REMOVE_DEFAULT_DSN: rimuovere la sezione specifica dell'origine dati predefinita dalle informazioni di sistema. (Rimuove anche la sezione specifica del driver predefinito dalla voce Odbcinst.ini nelle informazioni di sistema. Questo *fRequest* esegue la stessa funzione della funzione **obsoleta SQLRemoveDefaultDataSource.)** Quando questa opzione viene specificata, tutti gli altri parametri nella chiamata a **SQLConfigDataSource** devono essere valori DI Stanze nuSole; se non sono NULL, verranno ignorati.  
  
 *lpszDriver*  
 [Ingresso] Descrizione del driver (in genere il nome del DBMS associato) presentato agli utenti anziché il nome del driver fisico.  
  
 *LpszAttributi*  
 [Ingresso] Elenco doppiamente con terminazione null di attributi sotto forma di coppie parola chiave-valore. Per ulteriori informazioni, vedere [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo. Se non esiste alcuna voce nelle informazioni di sistema quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConfigDataSource** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido o NULL.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszDriver* non è valido. Non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave-valore non valide|L'argomento *lpszAttributes* contiene un errore di sintassi.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|Il programma di installazione non è in grado di eseguire l'operazione richiesta dall'argomento *fRequest.* La chiamata a **ConfigDSN** non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Impossibile caricare il driver o la libreria di installazione del convertitore|Impossibile caricare la libreria di installazione del driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLConfigDataSource** utilizza il valore di *lpszDriver* per leggere il percorso completo della DLL di installazione per il driver dalle informazioni di sistema. Carica la DLL e chiama **ConfigDSN** con gli stessi argomenti che gli sono stati passati.  
  
 **SQLConfigDataSource** restituisce FALSE se non è possibile trovare o caricare la DLL di installazione o se l'utente annulla la finestra di dialogo. In caso contrario, restituisce lo stato ricevuto da **ConfigDSN**.  
  
 **SQLConfigDataSource** esegue il mapping di DSN di sistema *fRequest*s al DSN utente *fRequest*s (ODBC_ADD_SYS_DSN a ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN a ODBC_CONFIG_DSN e ODBC_REMOVE_SYS_DSN a ODBC_REMOVE_DSN). Per distinguere i DSN utente e di sistema, **SQLConfigDataSource** imposta la modalità di configurazione del programma di installazione in base alla tabella seguente. Prima della restituzione, **SQLConfigDataSource** reimposta la modalità di configurazione su BOTHDSN. **ConfigDSN** (implementato dai driver) deve chiamare **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** per supportare un DSN di sistema. Per ulteriori informazioni, vedere [Funzione ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*fRichiesta*|Modalità di configurazione|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (nella DLL di installazione)|  
|Rimozione del nome di un'origine dati dalle informazioni di sistema|[ISTRUZIONE SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Aggiunta di un nome di origine dati alle informazioni di sistema|[Istruzione SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
