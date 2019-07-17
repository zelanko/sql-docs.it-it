---
title: Funzione SQLCreateDataSource | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3a6fced096c779b5ab91bf4e5b6a3f0a66e5f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121391"
---
# <a name="sqlcreatedatasource-function"></a>Funzione SQLCreateDataSource
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLCreateDataSource** Visualizza una finestra di dialogo con cui l'utente può aggiungere un'origine dati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwnd*  
 [Input] Handle della finestra padre.  
  
 *lpszDS*  
 [Input] Nome dell'origine dati. *lpszDS* può essere un puntatore null o una stringa vuota.  
  
## <a name="returns"></a>Valori di codice restituiti  
 **SQLCreateDataSource** restituisce TRUE se l'origine dati viene creato. In caso contrario, restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLCreateDataSource** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwnd* argomento era NULL o non valido.|  
|ODBC_ERROR_INVALID_DSN|DSN valido|Il *lpszDS* argomento è contenuta una stringa che non è valida per un DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|La chiamata a **ConfigDSN** con l'opzione ODBC_ADD_DSN non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Non è riuscito a caricare la libreria di programma di installazione driver o del convertitore.|Non è stato possibile caricare la libreria dell'installazione di driver.|  
|ODBC_ERROR_USER_CANCELED|Operazione annullata dall'utente|L'utente ha annullato la creazione di una nuova origine dati.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Non è possibile creare il DSN richiesto|Non è riuscito a connettersi al database. la chiamata a **SQLDriverConnect** per un DSN su File non ha restituito una connessione riuscita.<br /><br /> Impossibile scrivere nel file.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Se *hwnd* è null, **SQLCreateDataSource** restituisce FALSE. In caso contrario, viene visualizzato il **Crea nuova origine dati** finestra di dialogo con una pagina della procedura guidata per la scelta del tipo di origine dati da impostare, come illustrato nella figura seguente.  
  
 ![Creare la finestra di dialogo Nuova origine dati: selezionare il tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 L'opzione predefinita è **origine dati File**. Quando è stato scelto un'origine dati e **successivo** selezionato, viene visualizzata la pagina procedura guidata seguente che contiene un elenco di driver installati.  
  
 ![Creare la finestra di dialogo Nuova origine dati: selezione del driver](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Se **annullare** viene selezionata, la finestra di dialogo casella scompare e **SQLCreateDataSource** restituisce FALSE con il codice di errore di ODBC_ERROR_USER_CANCELED. Se il **origine dati utente** o **origine dati di sistema** è stata selezionata l'opzione, il **avanzate** pulsante non è disponibile.  
  
 Quando la **successivo** fa clic sul pulsante, si verificherà una delle opzioni seguenti, a seconda del tipo di dati è stata selezionata l'origine:  
  
-   Se **origine dati File** è stata selezionata, viene visualizzata una pagina di procedura guidata per l'utente di immettere un nome di file.  
  
-   Se uno dei due **origine dati utente** oppure **origine dati di sistema** è stata selezionata, viene visualizzata una pagina di procedura guidata che visualizza il tipo di origine dati e driver per la revisione e quando **fine** è si fa clic, l'origine dati è impostare.  
  
 Se **avanzate** si fa clic dalla pagina della procedura guidata Crea nuova origine dati, viene visualizzata una pagina della procedura guidata per l'utente di immettere informazioni specifiche del driver. Nella casella di testo della finestra di dialogo, digitare il driver e le parole chiave separate da restituisce, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Impostazioni di creazione DSN su File Advance](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Le parole chiave specifiche del driver aggiuntive sono reperibili sotto la descrizione del **SQLDriverConnect**. Tutti tranne **DSN** sono consentiti.  
  
 Il valore predefinito per il **Verifica connessione** opzione è TRUE. Questa impostazione predefinita viene applicata questa pagina della procedura guidata viene attivata o meno. Se **OK** viene selezionata, la stringa specificata nella casella di testo e il **Verifica connessione** vengono memorizzati nella cache il valore di opzione. (Se il **Close** pulsante o **Annulla** viene fatto clic su qualsiasi appena immesso informazioni specifiche del driver vengono perse perché la stringa specificata nella casella di testo e il **verificare questa connessione** valore dell'opzione non vengono memorizzate nella cache.)  
  
 Se **origine dati File** è stata selezionata nella pagina della procedura guidata prima, dopo che è stato selezionato un driver e i valori di parola chiave sono stati immessi nella pagina della procedura guidata avanzata, l'utente viene richiesto di immettere un nome file. Fare clic su **esplorare** per cercare un nome file, nel qual caso la directory predefinita nel **Sfoglia** casella viene specificata tramite la combinazione del percorso specificato da CommonFileDir in HKEY_LOCAL_MACHINE\SOFTWARE\ Microsoft\Windows\CurrentVersion e "ODBC\DataSources". (Se CommonFileDir era "C:\Program Files\Common Files", la directory predefinita potrebbe essere "C:\Programmi\Microsoft c:\Programmi\Common Files\ODBC\Data Sources").  
  
 Quando è stato immesso un nome di file e **successivo** viene fatto clic, il file nome immesso viene verificata la validità in base alle regole standard di denominazione dei file del sistema operativo. Se il nome del file non è valido, una finestra di messaggio di errore indica all'utente che sia stato immesso un nome di file non valido. Dopo che l'utente invia un acknowledgement per la finestra di messaggio, viene restituito lo stato attivo alla pagina della procedura guidata in cui viene immesso il nome del file. Se il nome del file è valido, viene visualizzata una pagina della procedura guidata che mostra le coppie parola chiave-valore selezionata per la revisione, come illustrato nella figura seguente.  
  
 ![Creare la finestra di dialogo Nuova origine dati: rivedere](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Se **Finish** si fa clic e **Zdroj dat File** è stato selezionato come tipo di origine dati e, se la **verificare la connessione** opzione è TRUE,  **SQLDriverConnect** viene chiamato con il **SAVEFILE** e **DRIVER** parole chiave. Il *DriverCompletion* argomento è impostato su SQL_DRIVER_COMPLETE. Il nome del file per il **SAVEFILE** parola chiave è il nome immesso o selezionato e il nome del driver per il **DRIVER** (parola chiave) è il nome che è stato scelto. Se una stringa di connessione specifici del driver è stata specificata nella pagina della procedura guidata avanzata, tale stringa viene aggiunto dopo il **DRIVER** (parola chiave).  
  
 Se **SQLDriverConnect** restituisce SQL_SUCCESS, gestione Driver ha creato il DSN su File. **SQLCreateDataSource** restituisce TRUE. Se **SQLDriverConnect** non viene restituito SQL_SUCCESS, un messaggio di avviso casella indica che non è stato possibile stabilire una connessione all'origine dati. È possibile creare comunque un DSN con informazioni di connessione minimo. Questa finestra di messaggio consente all'utente di annullare o continuare con la creazione DSN su File.  
  
 Se l'utente sceglie di continuare a creare il DSN, questo processo continua come se il **verificare la connessione** opzione fosse impostata su FALSE. Se l'utente sceglie di annullare, viene restituito FALSE per **SQLCreateDataSource** con un codice di errore di ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Se **origine dati File** è stato selezionato come tipo di origine dati e il **verificare questa connessione** opzione è FALSE, viene creato un DSN su File con il **DRIVER** (parola chiave) e specificato dall'utente stringa di connessione (se presente) dalla pagina della procedura guidata avanzata. Se la creazione di file ha esito positivo, viene restituito TRUE per **SQLCreateDataSource**. Se la creazione di file non ha esito positivo, una finestra di messaggio di errore indica all'utente con qualsiasi errore restituito dal sistema operativo. Viene restituito FALSE per **SQLCreateDataSource** con un codice di errore di ODBC_ERROR_CREATE_DSN_FAILED. Per altre informazioni sulle origini dati dei file, vedere [ci si connette tramite File Zdroje dat](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), oppure vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Se **utente** oppure **origine dati di sistema** è stato selezionato come il tipo di origine dati **ConfigDSN** nel programma di installazione driver della libreria viene chiamata con il ODBC_ADD_DSN  *trattano*. Per altre informazioni, vedere [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Gestione delle origini dati|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
