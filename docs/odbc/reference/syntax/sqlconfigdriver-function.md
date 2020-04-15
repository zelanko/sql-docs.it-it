---
title: Funzione SQLConfigDriver . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301246"
---
# <a name="sqlconfigdriver-function"></a>Funzione SQLConfigDriver
**Conformità**  
 Versione introdotta: ODBC 2.5  
  
 **Riepilogo**  
 **SQLConfigDriver** carica la DLL di installazione del driver appropriata e chiama la funzione **ConfigDriver.**  
  
 È inoltre possibile accedere alla funzionalità di **SQLConfigDriver** con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndPadre*  
 [Ingresso] Handle della finestra padre. La funzione non visualizzerà alcuna finestra di dialogo se l'handle è null.  
  
 *fRichiesta*  
 [Ingresso] Tipo di richiesta. *fRequest* deve contenere uno dei seguenti valori:  
  
 ODBC_CONFIG_DRIVER: modifica il timeout del pool di connessioni utilizzato dal driver.  
  
 ODBC_INSTALL_DRIVER: installa un nuovo driver.  
  
 ODBC_REMOVE_DRIVER: rimuove un driver esistente.  
  
 Questa opzione può anche essere specifica del driver, nel qual caso il *fRequest* per la prima opzione deve iniziare da ODBC_CONFIG_DRIVER_MAX1. Il *fRequest* per qualsiasi opzione aggiuntiva deve anche iniziare da un valore maggiore di ODBC_CONFIG_DRIVER_MAX .  
  
 *lpszDriver*  
 [Ingresso] Il nome del driver registrato nelle informazioni di sistema.  
  
 *lpszArgs (argomenti)*  
 [Ingresso] Stringa con terminazione null che contiene gli argomenti per un *oggetto fRequest*specifico del driver.  
  
 *lpszMsg*  
 [Uscita] Stringa con terminazione null che contiene un messaggio di output dall'installazione del driver.  
  
 *CbMsgMax*  
 [Ingresso] Lunghezza di *lpszMsg.*  
  
 *pcbMsgOut (informazioni in base al tanogra base del file*  
 [Uscita] Numero totale di byte disponibili da restituire in *lpszMsg*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbMsgMax*, il messaggio di output in *lpszMsg* viene troncato a *cbMsgMax* meno il carattere di terminazione null. L'argomento *pcbMsgOut* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConfigDriver** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszMsg* non è valido.|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> L'argomento *fRequest* era un'opzione specifica del driver minore o uguale a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszDriver* non è valido. Non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave-valore non valide|L'argomento *lpszArgs* contiene un errore di sintassi.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|Il programma di installazione non è in grado di eseguire l'operazione richiesta dall'argomento *fRequest.* La chiamata a **ConfigDriver** non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Impossibile caricare il driver o la libreria di installazione del convertitore|Impossibile caricare la libreria di installazione del driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLConfigDriver** consente a un'applicazione di chiamare la routine **ConfigDriver** di un driver senza dover conoscere il nome e caricare la DLL di installazione specifica del driver. Un programma di installazione chiama questa funzione dopo l'installazione della DLL di installazione del driver. Il programma chiamante deve essere consapevole del fatto che questa funzione potrebbe non essere disponibile per tutti i driver. In tal caso, il programma chiamante deve continuare senza errori.  
  
## <a name="driver-specific-options"></a>Opzioni specifiche del driver  
 Un'applicazione può richiedere funzionalità specifiche del driver esposte dal driver utilizzando il *fRequest* argomento. Il *fRequest* per la prima opzione sarà ODBC_CONFIG_DRIVER_MAX1 e le opzioni aggiuntive verranno incrementate di 1 da tale valore. Tutti gli argomenti richiesti dal driver per tale funzione devono essere forniti in una stringa con terminazione null passata nell'argomento *lpszArgs.* I driver che forniscono tale funzionalità devono mantenere una tabella di opzioni specifiche del driver. Le opzioni devono essere completamente documentate nella documentazione del driver. I writer di applicazioni che utilizzano opzioni specifiche del driver devono essere consapevoli del fatto che questo utilizzo renderà l'applicazione meno interoperabile.  
  
## <a name="setting-connection-pooling-timeout"></a>Impostazione del timeout del pool di connessioniSetting Connection Pooling Timeout  
 Le proprietà di timeout del pool di connessioni possono essere impostate quando si imposta la configurazione del driver. **SQLConfigDriver** viene chiamato con un *fRequest* di ODBC_CONFIG_DRIVER e *lpszArgs* impostato su **CPTimeout**. **CPTimeout** determina il periodo di tempo in cui una connessione può rimanere nel pool di connessioni senza essere utilizzata. Quando il timeout scade, la connessione viene chiusa e rimossa dal pool. Il timeout predefinito è 60 secondi.  
  
 Quando **SQLConfigDriver** viene chiamato con *fRequest* impostato su ODBC_INSTALL_DRIVER o ODBC_REMOVE_DRIVER, Gestione Driver carica la DLL di installazione del driver appropriato e chiama la funzione **ConfigDriver.** Quando **SQLConfigDriver** viene chiamato con un *fRequest* di ODBC_CONFIG_DRIVER, tutta l'elaborazione viene eseguita nel programma di installazione ODBC, in modo che la DLL di installazione del driver non deve essere caricata.  
  
## <a name="messages"></a>Messaggi  
 Una routine di installazione del driver può inviare un messaggio di testo a un'applicazione come stringhe con terminazione null nel buffer *lpszMsg.* Il messaggio verrà troncato a *cbMsgMax* meno il carattere di terminazione null dalla funzione **ConfigDriver** se è maggiore o uguale a *cbMsgMax* caratteri.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(nella DLL di installazione)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource (Origine datiSQLRemoveDefaultDataSource)](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
