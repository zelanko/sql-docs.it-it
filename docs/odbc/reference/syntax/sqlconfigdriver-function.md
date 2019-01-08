---
title: Funzione SQLConfigDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2b28b6380594150030e8f70a5b658a3bc18e258
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201770"
---
# <a name="sqlconfigdriver-function"></a>Funzione SQLConfigDriver
**Conformità**  
 Versione introdotta: ODBC 2.5  
  
 **Riepilogo**  
 **SQLConfigDriver** carica la DLL di installazione di driver appropriato e chiama le **ConfigDriver** (funzione).  
  
 La funzionalità del **SQLConfigDriver** sono accessibili anche con [ODBCCONF. File EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
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
 *hwndParent*  
 [Input] Handle della finestra padre. Se l'handle è null, la funzione non verrà visualizzata alcuna finestra di dialogo.  
  
 *trattano*  
 [Input] Tipo di richiesta. *trattano* deve contenere uno dei valori seguenti:  
  
 ODBC_CONFIG_DRIVER: Modifica il timeout utilizzato dal driver del pool.  
  
 ODBC_INSTALL_DRIVER: Installa un nuovo driver.  
  
 ODBC_REMOVE_DRIVER: Rimuove un driver esistente.  
  
 Questa opzione può anche essere specifici del driver, nel qual caso il *trattano* per la prima opzione deve iniziare da ODBC_CONFIG_DRIVER_MAX + 1. Il *trattano* per qualsiasi altra opzione è necessario anche avviare da un valore maggiore ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Input] Il nome del driver come registrato nelle informazioni di sistema.  
  
 *lpszArgs*  
 [Input] Stringa con terminazione null che contiene gli argomenti per una specifica del driver *trattano*.  
  
 *lpszMsg*  
 [Output] Una stringa con terminazione null che contiene un messaggio di output dal programma di installazione di driver.  
  
 *cbMsgMax*  
 [Input] Lunghezza di *lpszMsg.*  
  
 *pcbMsgOut*  
 [Output] Numero totale di byte disponibili per restituire *lpszMsg*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbMsgMax*, il messaggio di output in *lpszMsg* verrà troncato *cbMsgMax* meno la terminazione di tipo null carattere. Il *pcbMsgOut* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLConfigDriver** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszMsg* argomento non è valido.|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> Il *trattano* argomento era un'opzione di specifica del driver che era minore o uguale a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido. Non trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave / valore non valido|Il *lpszArgs* argomento contiene un errore di sintassi.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|Il programma di installazione non è stato possibile eseguire l'operazione richiesta per il *trattano* argomento. La chiamata a **ConfigDriver** non è riuscita.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Non è riuscito a caricare la libreria di programma di installazione driver o del convertitore.|Non è stato possibile caricare la libreria dell'installazione di driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLConfigDriver** consente a un'applicazione chiamare un driver **ConfigDriver** routine senza dover conoscere il nome e caricare la DLL di installazione specifici del driver. Un programma di installazione chiama questa funzione dopo l'installazione di driver che DLL è stata installata. Il programma chiamante deve tenere presente che questa funzione potrebbe non essere disponibile per tutti i driver. In tal caso, il programma chiamante deve continuare senza errori.  
  
## <a name="driver-specific-options"></a>Opzioni specifiche del driver  
 Un'applicazione può richiedere funzionalità specifiche del driver esposte dal driver tramite il *trattano* argomento. Il *trattano* per la prima opzione verrà ODBC_CONFIG_DRIVER_MAX + 1, e le opzioni aggiuntive verranno incrementate di 1 da tale valore. Eventuali argomenti richiesti dal driver per tale funzione deve essere fornita in una stringa con terminazione null passato il *lpszArgs* argomento. I driver che fornisce questa funzionalità è necessario gestire una tabella delle opzioni specifiche del driver. Le opzioni devono essere completamente documentate nella documentazione del driver. Gli autori di applicazioni che usano le opzioni specifiche del driver devono essere consapevoli che questo uso effettuerà l'applicazione meno interoperativa.  
  
## <a name="setting-connection-pooling-timeout"></a>L'impostazione di Timeout pool di connessioni  
 Quando si imposta la configurazione del driver, è possono impostare le proprietà di timeout pool di connessioni. **SQLConfigDriver** viene chiamato con un *trattano* di ODBC_CONFIG_DRIVER e *lpszArgs* impostata **CPTimeout**. **CPTimeout** determina il periodo di tempo che una connessione può rimanere nel pool di connessioni senza essere utilizzati. Quando il timeout scade, la connessione viene chiusa e rimossi dal pool. Il timeout predefinito è 60 secondi.  
  
 Quando **SQLConfigDriver** viene chiamato con *trattano* impostato su ODBC_INSTALL_DRIVER o ODBC_REMOVE_DRIVER, gestione Driver carica la DLL di installazione di driver appropriato e chiama il  **ConfigDriver** (funzione). Quando **SQLConfigDriver** viene chiamato con un *trattano* di ODBC_CONFIG_DRIVER, tutta l'elaborazione viene eseguita nel programma di installazione ODBC, in modo che la DLL di installazione di driver non deve essere caricato.  
  
## <a name="messages"></a>Messaggi  
 Una routine di installazione di driver può inviare un messaggio di testo a un'applicazione sotto forma di stringhe con terminazione null nel *lpszMsg* buffer. Il messaggio verrà troncato a *cbMsgMax* meno il carattere di terminazione null per il **ConfigDriver** funzione se è maggiore o uguale a *cbMsgMax* caratteri.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(nel programma di installazione DLL)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
