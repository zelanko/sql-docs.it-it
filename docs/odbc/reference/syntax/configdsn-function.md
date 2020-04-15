---
title: Funzione ConfigDSN . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbae126c819088bd277621b207454503a86c8955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306042"
---
# <a name="configdsn-function"></a>Funzione ConfigDSN
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **ConfigDSN** aggiunge, modifica o elimina origini dati dalle informazioni di sistema. Potrebbe richiedere all'utente le informazioni di connessione. Può trovarsi nella DLL del driver o in una DLL di installazione separata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigDSN(  
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
  
 ODBC_ADD_DSN: aggiungere una nuova origine dati.  
  
 ODBC_CONFIG_DSN: configurare (modificare) un'origine dati esistente.  
  
 ODBC_REMOVE_DSN: rimuovere un'origine dati esistente.  
  
 *lpszDriver*  
 [Ingresso] Descrizione del driver (in genere il nome del DBMS associato) presentato agli utenti anziché il nome del driver fisico.  
  
 *LpszAttributi*  
 [Ingresso] Elenco doppiamente con terminazione null di attributi sotto forma di coppie parola chiave-valore. Per ulteriori informazioni, vedere "Commenti".  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigDSN** restituisce FALSE, un valore * \*pfErrorCode* associato viene inviato nel buffer degli errori del programma di installazione da una chiamata a **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave-valore non valide|L'argomento *lpszAttributes* contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszDriver* non è valido. Non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|Impossibile eseguire l'operazione richiesta dall'argomento *fRequest.*|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o del traduttore|Errore specifico del driver per il quale non è presente alcun errore definito del programma di installazione ODBC. *L'argomento SzError* in una chiamata alla funzione **SQLPostInstallerError** deve contenere il messaggio di errore specifico del driver.|  
  
## <a name="comments"></a>Commenti  
 **ConfigDSN** riceve le informazioni di connessione dalla DLL del programma di installazione come un elenco di attributi sotto forma di coppie parola chiave-valore. Ogni coppia viene terminata con un byte null e l'intero elenco viene terminato con un byte null. (Ovvero, due byte null segnano la fine dell'elenco.) Gli spazi non sono consentiti intorno al segno di uguale nella coppia parola chiave-valore. **ConfigDSN** può accettare parole chiave che non sono parole chiave valide per **SQLBrowseConnect** e **SQLDriverConnect**. **ConfigDSN** non supporta necessariamente tutte le parole chiave valide per **SQLBrowseConnect** e **SQLDriverConnect**. **(ConfigDSN** non accetta la parola chiave **DRIVER.)** Le parole chiave utilizzate dalla funzione **ConfigDSN** devono supportare tutte le opzioni necessarie per ricreare l'origine dati utilizzando la funzionalità di installazione AUTO del programma di installazione. Quando gli utilizzi dei valori **ConfigDSN** e dei valori della stringa di connessione sono uguali, è necessario usare le stesse parole chiave.  
  
 Come in **SQLBrowseConnect** e **SQLDriverConnect**, le parole chiave e i relativi valori non devono contenere **[]{}(),;? E \*** il valore della parola chiave **DSN** non può essere costituito solo da spazi vuoti. A causa della grammatica del Registro di sistema,\\le parole chiave e i nomi delle origini dati non possono contenere il carattere barra rovesciata ( ).  
  
 **ConfigDSN** deve chiamare **SQLValidDSN** per controllare la lunghezza del nome dell'origine dati e per verificare che non siano inclusi caratteri non validi nel nome. Se il nome dell'origine dati è più lungo di SQL_MAX_DSN_LENGTH o include caratteri non validi, **SQLValidDSN** restituisce un errore e **ConfigDSN** restituisce un errore. La lunghezza del nome dell'origine dati viene controllata anche da **SQLWriteDSNToIni**.  
  
 Ad esempio, per configurare un'origine dati che richiede un ID utente, una password e un nome di database, un'applicazione di installazione potrebbe passare le seguenti coppie parola chiave-valore:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Per altre informazioni su queste parole chiave, vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) e la documentazione di ogni driver.  
  
 Per visualizzare una finestra di dialogo, *hwndParent* non deve essere null.  
  
## <a name="adding-a-data-source"></a>Aggiunta di un'origine dati  
 Se il nome di un'origine dati viene passato a **ConfigDSN** in *lpszAttributes*, **ConfigDSN** verifica che il nome sia valido. Se il nome dell'origine dati corrisponde a un nome di origine dati esistente e *hwndParent* è null, **ConfigDSN** sovrascrive il nome esistente. Se corrisponde a un nome esistente e *hwndParent* non è null, **ConfigDSN** richiede all'utente di sovrascrivere il nome esistente.  
  
 Se *lpszAttributes* contiene informazioni sufficienti per connettersi a un'origine dati, **ConfigDSN** può aggiungere l'origine dati o visualizzare una finestra di dialogo con cui l'utente può modificare le informazioni di connessione. Se *lpszAttributes* non contiene informazioni sufficienti per connettersi a un'origine dati, **ConfigDSN** deve determinare le informazioni necessarie. Se *hwndParent* non è null, viene visualizzata una finestra di dialogo per recuperare le informazioni dall'utente.  
  
 Se **ConfigDSN** visualizza una finestra di dialogo, deve visualizzare tutte le informazioni di connessione passate in *lpszAttributes*. In particolare, se è stato passato un nome di origine dati, **ConfigDSN** visualizza tale nome ma non consente all'utente di modificarlo. **ConfigDSN** può fornire valori predefiniti per le informazioni di connessione non passate in *lpszAttributes*.  
  
 Se **ConfigDSN** non è in grado di ottenere informazioni di connessione complete per un'origine dati, restituisce FALSE.  
  
 Se **ConfigDSN** può ottenere informazioni di connessione complete per un'origine dati, chiama **SQLWriteDSNToIni** nella DLL del programma di installazione per aggiungere la nuova specifica dell'origine dati al file Odbc.ini (o al Registro di sistema). **SQLWriteDSNToIni** aggiunge il nome dell'origine dati alla sezione [Origini dati ODBC], crea la sezione specifica dell'origine dati e aggiunge la parola chiave **DRIVER** con la descrizione del driver come valore. **ConfigDSN** chiama **SQLWritePrivateProfileString** nella DLL del programma di installazione per aggiungere eventuali parole chiave e valori aggiuntivi utilizzati dal driver.  
  
## <a name="modifying-a-data-source"></a>Modifica di un'origine datiModifying a Data Source  
 Per modificare un'origine dati, è necessario passare un nome di origine dati a **ConfigDSN** in *lpszAttributes*. **ConfigDSN** verifica che il nome dell'origine dati si trova nel file Odbc.ini (o Registro di sistema).  
  
 Se *hwndParent* è null, **ConfigDSN** utilizza le informazioni in *lpszAttributes* per modificare le informazioni nel file Odbc.ini (o Registro di sistema). Se *hwndParent* non è null, **ConfigDSN** visualizza una finestra di dialogo utilizzando le informazioni in *lpszAttributes*; per informazioni non presenti in *lpszAttributes*, vengono utilizzate le informazioni provenienti dalle informazioni di sistema. L'utente può modificare le informazioni prima **che ConfigDSN le** memorizzi nelle informazioni di sistema.  
  
 Se il nome dell'origine dati è stato modificato, **ConfigDSN** chiama innanzitutto **SQLRemoveDSNFromIni** nella DLL del programma di installazione per rimuovere la specifica dell'origine dati esistente dal file Odbc.ini (o dal Registro di sistema). Segue quindi i passaggi nella sezione precedente per aggiungere la nuova specifica dell'origine dati. Se il nome dell'origine dati non è stato modificato, **ConfigDSN** chiama **SQLWritePrivateProfileString** nella DLL del programma di installazione per apportare altre modifiche. **ConfigDSN** potrebbe non eliminare o modificare il valore della parola chiave **Driver.**  
  
## <a name="deleting-a-data-source"></a>Eliminazione di un'origine datiDeleting a Data Source  
 Per eliminare un'origine dati, è necessario passare un nome di origine dati a **ConfigDSN** in *lpszAttributes*. **ConfigDSN** verifica che il nome dell'origine dati si trova nel file Odbc.ini (o Registro di sistema). Chiama quindi **SQLRemoveDSNFromIni** nella DLL del programma di installazione per rimuovere l'origine dati.  
  
## <a name="note"></a>Note
 Se si scrive una versione Unicode di questa routine, deve essere denominata **ConfigDSNW**, con argomenti LPCWSTR anziché LPCSTR.
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Recupero di un valore dal file Odbc.ini o dal Registro di sistema|[OGGETTO SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource (Origine datiSQLRemoveDefaultDataSource)](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Rimozione di un nome di origine dati da Odbc.ini (o Registro di sistema)|[ISTRUZIONE SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Aggiunta di un nome di origine dati a Odbc.ini (o Registro di sistema)|[Istruzione SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Scrittura di un valore nel file Odbc.ini o nel Registro di sistema|[OGGETTO SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
