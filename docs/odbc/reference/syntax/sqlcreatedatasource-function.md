---
title: Funzione SQLCreateDataSource . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301201"
---
# <a name="sqlcreatedatasource-function"></a>Funzione SQLCreateDataSource
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLCreateDataSource** visualizza una finestra di dialogo con cui l'utente può aggiungere un'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hwnd*  
 [Ingresso] Handle della finestra padre.  
  
 *lpszDS*  
 [Ingresso] Nome dell'origine dati. *lpszDS* può essere un puntatore null o una stringa vuota.  
  
## <a name="returns"></a>Valori di codice restituiti  
 **SQLCreateDataSource** restituisce TRUE se viene creata l'origine dati. In caso contrario, restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCreateDataSource** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwnd* non è valido o NULL.|  
|ODBC_ERROR_INVALID_DSN|DSN non valido|L'argomento *lpszDS* contiene una stringa non valida per un DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|La chiamata a **ConfigDSN** con l'opzione ODBC_ADD_DSN non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Impossibile caricare il driver o la libreria di installazione del convertitore|Impossibile caricare la libreria di installazione del driver.|  
|ODBC_ERROR_USER_CANCELED|Operazione annullata dall'utente|Creazione annullata dall'utente di una nuova origine dati.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Impossibile creare il DSN richiesto|Impossibile connettersi al database. la chiamata a **SQLDriverConnect** per un DSN file non ha restituito una connessione riuscita.<br /><br /> Impossibile scrivere nel file.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Se *hwnd* è null, **SQLCreateDataSource** restituisce FALSE. In caso contrario, viene visualizzata la finestra di dialogo **Crea nuova origine dati** con una pagina della procedura guidata per scegliere il tipo di origine dati da configurare, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Crea nuova origine dati: selezione del tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 L'opzione predefinita è **Origine dati file**. Quando si sceglie un'origine dati e si fa clic su **Avanti,** viene visualizzata la seguente pagina della procedura guidata contenente un elenco dei driver installati.  
  
 ![Finestra di dialogo Crea nuova origine dati: selezione del driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se si fa clic su **Annulla,** la finestra di dialogo scompare e **SQLCreateDataSource** restituisce FALSE con il codice di errore di ODBC_ERROR_USER_CANCELED. Se è stata selezionata l'opzione **Origine dati utente** o Origine **dati** di sistema, il pulsante **Avanzate** non è disponibile.  
  
 Quando si fa clic sul pulsante **Avanti,** si verifica una delle situazioni seguenti, a seconda del tipo di origine dati selezionato:  
  
-   Se è stata selezionata **l'opzione Origine dati file,** viene visualizzata una pagina della procedura guidata in cui l'utente può immettere un nome file.  
  
-   Se è stata selezionata **l'opzione Origine dati utente** o Origine **dati** di sistema, viene visualizzata una pagina della procedura guidata che visualizza il tipo di origine dati e il driver per la revisione e quando si fa clic su **Fine,** l'origine dati viene impostata.  
  
 Se si fa clic su **Avanzate** nella pagina della procedura guidata Crea nuova origine dati, viene visualizzata una pagina della procedura guidata in cui l'utente può immettere informazioni specifiche del driver. Nella casella di testo di questa finestra di dialogo digitare il driver e le parole chiave separate da resi, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Impostazioni avanzate creazione DNS su file](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Ulteriori parole chiave specifiche del driver sono disponibili nella descrizione di **SQLDriverConnect**. Sono consentiti tutti tranne **DSN.**  
  
 L'impostazione predefinita per l'opzione **Verifica connessione** è TRUE. Questa impostazione predefinita si applica indipendentemente dall'attivazione di questa pagina della procedura guidata. Se si fa clic su **OK,** la stringa specificata nella casella di testo e il valore dell'opzione **Verifica connessione** vengono memorizzati nella cache. Se si fa clic sul pulsante **Chiudi** o **Annulla,** tutte le informazioni specifiche del driver appena immesse vengono perse perché la stringa specificata nella casella di testo e il valore dell'opzione **Verifica connessione** non vengono memorizzati nella cache.  
  
 Se origine **dati file** è stata selezionata nella prima pagina della procedura guidata, dopo che è stato selezionato un driver e i valori delle parole chiave sono stati immessi nella pagina avanzata della procedura guidata, all'utente viene richiesto di immettere un nome di file. Fare clic su **Sfoglia** per cercare un nome di file, nel qual caso la directory predefinita nella casella **Sfoglia** è specificata da una combinazione del percorso specificato da CommonFileDir in HKEY_LOCAL_MACHINE SOFTWARE . (Se CommonFileDir era "C:"Programmi "File comuni", la directory predefinita sarà "C:.  
  
 Quando viene immesso un nome di file e si fa clic su **Avanti,** viene verificata la validità del nome del file immesso rispetto alle regole standard di denominazione dei file del sistema operativo. Se il nome del file non è valido, una finestra di messaggio di errore notifica all'utente che è stato immesso un nome di file non valido. Dopo che l'utente riconosce la finestra di messaggio, lo stato attivo viene restituito alla pagina della procedura guidata in cui viene immesso il nome del file. Se il nome del file è valido, viene visualizzata una pagina della procedura guidata che mostra le coppie parola chiave-valore selezionate per la revisione, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Crea nuova origine dati: verifica](../../../odbc/reference/syntax/media/ch23d.gif "CH23D (in inglese)")  
  
 Se si fa clic su **Fine** ed è stato selezionato **Origine dati file** come tipo di origine dati e se l'opzione Verifica **connessione** è TRUE, **SQLDriverConnect** viene chiamato con le parole chiave **SAVEFILE** e **DRIVER.** L'argomento *DriverCompletion* è impostato su SQL_DRIVER_COMPLETE. Il nome file per la parola chiave **SAVEFILE** è il nome immesso o scelto e il nome del driver per la parola chiave **DRIVER** è il nome scelto. Se nella pagina della procedura guidata Avanzate è stata specificata una stringa di connessione specifica del driver, tale stringa viene aggiunta dopo la parola chiave **DRIVER.**  
  
 Se **SQLDriverConnect** restituisce SQL_SUCCESS, Gestione Driver ha creato il DSN file. **SQLCreateDataSource** restituisce TRUE. Se **SQLDriverConnect** non restituisce SQL_SUCCESS, una finestra di messaggio di avviso indica che non è stato possibile creare una connessione all'origine dati. È comunque possibile creare un DSN con informazioni di connessione minime. Questa finestra di messaggio consente all'utente di annullare o continuare con la creazione del DSN su file.  
  
 Se l'utente sceglie di continuare a creare il DSN, questo processo continua come se l'opzione **Verifica questa connessione** fosse impostata su FALSE. Se l'utente sceglie di annullare, FALSE viene restituito per **SQLCreateDataSource** con un codice di errore di ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se **origine dati file** è stato selezionato come tipo di origine dati e l'opzione Verifica questa **connessione** è FALSE, viene creato un DSN file con la parola chiave **DRIVER** e la stringa di connessione specificata dall'utente (se presente) dalla pagina della procedura guidata Avanzate. Se la creazione del file ha avuto esito positivo, TRUE viene restituito per **SQLCreateDataSource**. Se la creazione del file non è riuscita, una finestra di messaggio di errore notifica all'utente con qualsiasi errore è stato restituito dal sistema operativo. FALSE viene restituito per **SQLCreateDataSource** con un codice di errore di ODBC_ERROR_CREATE_DSN_FAILED. Per ulteriori informazioni sulle origini dati su file, vedere [Connessione tramite origini dati file](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se è stato selezionato **Utente** o **Origine dati** di sistema come tipo di origine dati, **ConfigDSN** nella libreria di installazione del driver viene chiamato con il ODBC_ADD_DSN *fRequest*. Per ulteriori informazioni, vedere [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Gestione delle origini dati|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
