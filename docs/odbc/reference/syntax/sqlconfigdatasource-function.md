---
title: Funzione SQLConfigDataSource | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7706d3a7dd05273b4608d49211a6eaab8927f2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118613"
---
# <a name="sqlconfigdatasource-function"></a>Funzione SQLConfigDataSource
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLConfigDataSource** aggiunge, modifica o Elimina le origini dati.  
  
 La funzionalità del **SQLConfigDataSource** sono accessibili anche con [ODBCCONF. File EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndParent*  
 [Input] Handle della finestra padre. Se l'handle è null, la funzione non verrà visualizzata alcuna finestra di dialogo.  
  
 *fRequest*  
 [Input] Tipo di richiesta. Il *trattano* argomento deve essere uno dei valori seguenti:  
  
 ODBC_ADD_DSN: Aggiungere una nuova origine dati utente.  
  
 ODBC_CONFIG_DSN: Configurare (modificare) un'origine dati utente esistente.  
  
 ODBC_REMOVE_DSN: Rimuovere un'origine dati utente esistente.  
  
 ODBC_ADD_SYS_DSN: Aggiungere una nuova origine dati di sistema.  
  
 ODBC_CONFIG_SYS_DSN: Modificare un'origine dati di sistema esistente.  
  
 ODBC_REMOVE_SYS_DSN: Rimuovere un'origine dati di sistema esistente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Rimuovere la sezione di specifica origine dati predefinita dalle informazioni di sistema. (Rimuove inoltre la sezione specifica di driver predefiniti dalla voce Odbcinst. ini nelle informazioni di sistema. Ciò *trattano* esegue la stessa funzione deprecata **SQLRemoveDefaultDataSource** (funzione).) Quando questa opzione viene specificata, tutti gli altri parametri nella chiamata a **SQLConfigDataSource** devono essere valori null; se non sono NULL, queste verranno ignorate.  
  
 *lpszDriver*  
 [Input] Descrizione del driver (in genere il nome del sistema DBMS associati) presentato agli utenti anziché il nome del driver fisico.  
  
 *lpszAttributes*  
 [Input] Un elenco di attributi in forma di coppie valore-parola chiave doppia terminazione null. Per altre informazioni, vedere [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore. Se le informazioni di sistema non esiste alcuna voce quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConfigDataSource** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento era NULL o non valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido. Non trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave / valore non valido|Il *lpszAttributes* argomento contiene un errore di sintassi.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|Il programma di installazione non è stato possibile eseguire l'operazione richiesta per il *trattano* argomento. La chiamata a **ConfigDSN** non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Non è riuscito a caricare la libreria di programma di installazione driver o del convertitore.|Non è stato possibile caricare la libreria dell'installazione di driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLConfigDataSource** utilizza il valore di *lpszDriver* per leggere il percorso completo della DLL di installazione per il driver dalle informazioni di sistema. Carica la DLL e chiama **ConfigDSN** con gli stessi argomenti passati a esso.  
  
 **SQLConfigDataSource** restituisce FALSE se non è in grado di trovare o caricare la DLL di installazione o se l'utente annulla la finestra di dialogo. In caso contrario, restituisce lo stato ricevuta dal **ConfigDSN**.  
  
 **SQLConfigDataSource** esegue il mapping di DSN di sistema *trattano*s per il DSN utente *trattano*s (ODBC_ADD_SYS_DSN a ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN e ODBC_REMOVE_SYS_ DSN a ODBC_REMOVE_DSN). Per distinguere i DSN di sistema e utente **SQLConfigDataSource** imposta il programma di installazione in modalità di configurazione in base alla tabella riportata di seguito. Prima della restituzione, **SQLConfigDataSource** BOTHDSN Reimposta modalità di configurazione. **ConfigDSN** (implementato dal driver) deve chiamare **SQLWriteDSNToIni** e **SQLWritePrivateProfileString** per supportare un DSN di sistema. Per altre informazioni, vedere [funzione ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*fRequest*|Modalità di configurazione|  
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
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (nel programma di installazione DLL)|  
|Rimozione di un nome dell'origine dati dalle informazioni di sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Aggiunta di un nome dell'origine dati per le informazioni di sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
