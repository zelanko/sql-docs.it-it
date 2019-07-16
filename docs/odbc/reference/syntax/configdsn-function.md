---
title: Funzione ConfigDSN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 78be24ea75fad04c7b7c1bdae103dfd3f92c78ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016722"
---
# <a name="configdsn-function"></a>Funzione ConfigDSN
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **ConfigDSN** aggiunge, modifica o Elimina le origini dati dalle informazioni di sistema. Possono richiedere all'utente le informazioni di connessione. Può essere nella DLL del driver o una DLL di installazione separato.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigDSN(  
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
  
 ODBC_ADD_DSN: Aggiungere una nuova origine dati.  
  
 ODBC_CONFIG_DSN: Configurare (modificare) un'origine dati esistente.  
  
 ODBC_REMOVE_DSN: Rimuovere un'origine dati esistente.  
  
 *lpszDriver*  
 [Input] Descrizione del driver (in genere il nome del sistema DBMS associati) presentato agli utenti anziché il nome del driver fisico.  
  
 *lpszAttributes*  
 [Input] Un elenco di attributi in forma di coppie valore-parola chiave doppia terminazione null. Per altre informazioni, vedere "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigDSN** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore viene inserito nel buffer di errore di programma di installazione da una chiamata al **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento non è valido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave / valore non valido|Il *lpszAttributes* argomento contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido. Non trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|Non è stato possibile eseguire l'operazione richiesta per il *trattano* argomento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o Microsoft translator|Un errore specifico del driver per cui non si verificano errori di programma di installazione ODBC definita. Il *SzError* argomento in una chiamata per il **SQLPostInstallerError** (funzione) deve contenere il messaggio di errore specifico del driver.|  
  
## <a name="comments"></a>Commenti  
 **ConfigDSN** riceve le informazioni di connessione dal programma di installazione DLL come un elenco di attributi in forma di coppie parola chiave / valore. Ogni coppia viene terminata con un byte null e l'intero elenco viene terminata con un byte null. (Vale a dire, due byte null contrassegnano la fine dell'elenco.) Non sono consentiti spazi prima e dopo il segno di uguale nella coppia parola chiave / valore. **ConfigDSN** può accettare parole chiave che non sono parole chiave valide **SQLBrowseConnect** e **SQLDriverConnect**. **ConfigDSN** sono non necessariamente supportati tutte le parole chiave che sono parole chiave valide **SQLBrowseConnect** e **SQLDriverConnect**. (**ConfigDSN** non accetta le **DRIVER** parola chiave.) Le parole chiave utilizzate per la **ConfigDSN** funzione deve supportare tutte le opzioni necessarie per ricreare l'origine dati usando la funzionalità di installazione automatica del programma di installazione. Quando gli utilizzi del **ConfigDSN** valori e i valori di stringa di connessione sono uguali, è necessario usare le stesse parole chiave.  
  
 Come in **SQLBrowseConnect** e **SQLDriverConnect**, le parole chiave e i relativi valori non devono contenere il **[]{}(),? \*=! @** caratteri e il valore della **DSN** parola chiave non può essere costituito solo da spazi vuoti. A causa la grammatica del Registro di sistema, i nomi delle origini dati e le parole chiave non può contenere la barra rovesciata (\\) caratteri.  
  
 **ConfigDSN** chiami **SQLValidDSN** per controllare la lunghezza del nome dell'origine dati e per verificare che non siano inclusi caratteri validi nel nome. Se il nome dell'origine dati è più lungo di SQL_MAX_DSN_LENGTH o includono caratteri non validi, **SQLValidDSN** restituisce un errore e **ConfigDSN** restituisce un errore. La lunghezza del nome dell'origine dati è anche di verificarlo **SQLWriteDSNToIni**.  
  
 Per configurare un'origine dati che richiede un ID utente, password e nome del database, ad esempio, un'applicazione di installazione potrebbe passare le coppie parola chiave / valore seguente:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Per altre informazioni sulle parole chiave, vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) e ogni relativa documentazione.  
  
 Per visualizzare una finestra di dialogo *hwndParent* non deve essere null.  
  
## <a name="adding-a-data-source"></a>Aggiunta di un'origine dati  
 Se un nome dell'origine dati viene passato a **ConfigDSN** nelle *lpszAttributes*, **ConfigDSN** verifica che il nome sia valido. Se il nome dell'origine dati corrisponde a un nome di origine dati esistente e *hwndParent* è null, **ConfigDSN** sovrascrive il nome esistente. Se corrisponde a un nome esistente e *hwndParent* non è null, **ConfigDSN** richiesto all'utente di sovrascrivere il nome esistente.  
  
 Se *lpszAttributes* contiene informazioni sufficienti per connettersi a un'origine dati, **ConfigDSN** può aggiungere l'origine dati o visualizzare una finestra di dialogo con cui l'utente può modificare le informazioni di connessione. Se *lpszAttributes* non contiene informazioni sufficienti per connettersi a un'origine dati, **ConfigDSN** necessario determinare le informazioni necessarie; se *hwndParent* non è null, viene visualizzata una finestra di dialogo per recuperare le informazioni da parte dell'utente.  
  
 Se **ConfigDSN** consente di visualizzare una finestra di dialogo deve visualizzare le informazioni di connessione passate nel *lpszAttributes*. In particolare, se un nome dell'origine dati è stato passato a essa **ConfigDSN** visualizza tale nome, ma non consente all'utente di modificarlo. **ConfigDSN** può fornire valori predefiniti per le informazioni di connessione non passato nel *lpszAttributes*.  
  
 Se **ConfigDSN** non è possibile ottenere le informazioni di connessione completa per un'origine dati, restituisce FALSE.  
  
 Se **ConfigDSN** possono ottenere informazioni di connessione completa per un'origine dati, chiama **SQLWriteDSNToIni** nel programma di installazione DLL per aggiungere la nuova specifica origine dati del file ini (o del Registro di sistema). **SQLWriteDSNToIni** aggiunge il nome dell'origine dati alla sezione [origini dati ODBC], la sezione specifica di origine dati crea e aggiunge i **DRIVER** (parola chiave) con la descrizione del driver come relativo valore. **ConfigDSN** chiamate **SQLWritePrivateProfileString** nel programma di installazione DLL per aggiungere delle parole chiave aggiuntive e i valori utilizzati dal driver.  
  
## <a name="modifying-a-data-source"></a>Modifica di un'origine dati  
 Per modificare un'origine dati, è necessario passare un nome dell'origine dati **ConfigDSN** nelle *lpszAttributes*. **ConfigDSN** verifica che il nome dell'origine dati sia nel file ini (o del Registro di sistema).  
  
 Se *hwndParent* è null, **ConfigDSN** utilizza le informazioni nelle *lpszAttributes* per modificare le informazioni nel file ODBC ini (o del Registro di sistema). Se *hwndParent* non è null, **ConfigDSN** consente di visualizzare una finestra di dialogo usando le informazioni delle *lpszAttributes*; per informazioni non in *lpszAttributes* , Usa informazioni dalle informazioni di sistema. Gli utenti possono modificare le informazioni prima **ConfigDSN** archivia le informazioni di sistema.  
  
 Se il nome dell'origine dati è stato modificato, **ConfigDSN** chiama innanzitutto **SQLRemoveDSNFromIni** nel programma di installazione DLL per rimuovere i dati esistenti di origine specifica dal file ini (o del Registro di sistema). Ne consegue quindi i passaggi nella sezione precedente per aggiungere la nuova specifica origine dati. Se il nome dell'origine dati non è stato modificato, **ConfigDSN** chiamate **SQLWritePrivateProfileString** nel programma di installazione DLL per apportare altre modifiche. **ConfigDSN** non può eliminare o modificare il valore della **Driver** (parola chiave).  
  
## <a name="deleting-a-data-source"></a>Eliminazione di un'origine dati  
 Per eliminare un'origine dati, è necessario passare un nome dell'origine dati **ConfigDSN** nelle *lpszAttributes*. **ConfigDSN** verifica che il nome dell'origine dati sia nel file ini (o del Registro di sistema). Chiama poi **SQLRemoveDSNFromIni** nel programma di installazione DLL per rimuovere l'origine dati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Ottiene un valore dal file ini o nel Registro di sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Rimozione di un nome dell'origine dati da ODBC. ini (o del Registro di sistema)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Aggiunta di un nome dell'origine dati ODBC. ini (o del Registro di sistema)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Scrive un valore per il file ODBC ini o nel Registro di sistema|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
