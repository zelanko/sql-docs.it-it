---
title: Funzione ConfigDriver . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303962"
---
# <a name="configdriver-function"></a>Funzione ConfigDriver
**Conformità**  
 Versione introdotta: ODBC 2.5  
  
 **Riepilogo**  
 **ConfigDriver** consente a un programma di installazione di eseguire funzioni di installazione e disinstallazione senza richiedere che il programma **chiami ConfigDSN**. Questa funzione eseguirà funzioni specifiche del driver, ad esempio la creazione di informazioni di sistema specifiche del driver e l'esecuzione di conversioni DSN durante l'installazione, nonché la pulizia delle modifiche alle informazioni di sistema durante la disinstallazione. Questa funzione è esposta dalla DLL di installazione del driver o da una DLL di installazione separata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndPadre*  
 [Ingresso] Handle della finestra padre. La funzione non visualizzerà alcuna finestra di dialogo se l'handle è null.  
  
 *fRichiesta*  
 [Ingresso] Tipo di richiesta. L'argomento *fRequest* deve contenere uno dei valori seguenti:  
  
 ODBC_INSTALL_DRIVER: installare un nuovo driver.  
  
 ODBC_REMOVE_DRIVER: rimuovere un driver.  
  
 Questa opzione può anche essere specifica del driver, nel qual caso l'argomento *fRequest* per la prima opzione deve iniziare da ODBC_CONFIG_DRIVER_MAX1. Anche l'argomento *fRequest* per qualsiasi opzione aggiuntiva deve iniziare da un valore maggiore di ODBC_CONFIG_DRIVER_MAX.  
  
 *lpszDriver*  
 [Ingresso] Nome del driver registrato nella chiave Odbcinst.ini delle informazioni di sistema.  
  
 *lpszArgs (argomenti)*  
 [Ingresso] Stringa con terminazione null contenente gli argomenti per un *oggetto fRequest*specifico del driver.  
  
 *lpszMsg*  
 [Uscita] Stringa con terminazione null contenente un messaggio di output dall'installazione del driver.  
  
 *CbMsgMax*  
 [Ingresso] Lunghezza di *lpszMsg*.  
  
 *pcbMsgOut (informazioni in base al tanogra base del file*  
 [Uscita] Numero totale di byte disponibili da restituire in *lpszMsg*.  
  
 Se il numero di byte disponibili da restituire è maggiore o uguale a *cbMsgMax*, il messaggio di output in *lpszMsg* viene troncato a *cbMsgMax* meno il carattere di terminazione null. L'argomento *pcbMsgOut* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigDriver** restituisce FALSE, un valore * \*pfErrorCode* associato viene inviato al buffer degli errori del programma di installazione da una chiamata a **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> L'opzione specifica del driver era minore o uguale a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszDriver* non è valido. Non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|Impossibile eseguire l'operazione richiesta dall'argomento *fRequest.*|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o del traduttore|Errore specifico del driver per il quale non è presente alcun errore definito del programma di installazione ODBC. *L'argomento SzError* in una chiamata alla funzione **SQLPostInstallerError** deve contenere il messaggio di errore specifico del driver.|  
  
## <a name="comments"></a>Commenti  
  
### <a name="driver-specific-options"></a>Opzioni specifiche del driver  
 Un'applicazione può richiedere funzionalità specifiche del driver esposte dal driver utilizzando il *fRequest* argomento. Il *fRequest* per la prima opzione sarà ODBC_CONFIG_DRIVER_MAX più 1 e le opzioni aggiuntive verranno incrementate di 1 da tale valore. Tutti gli argomenti richiesti dal driver per tale funzione devono essere forniti in una stringa con terminazione null passata nell'argomento *lpszArgs.* I driver che forniscono tale funzionalità devono mantenere una tabella di opzioni specifiche del driver. Le opzioni devono essere completamente documentate nella documentazione del driver. I writer di applicazioni che utilizzano opzioni specifiche del driver devono essere consapevoli del fatto che questa operazione renderà l'applicazione meno interoperabile.  
  
### <a name="messages"></a>Messaggi  
 Una routine di installazione del driver può inviare un messaggio di testo a un'applicazione come stringa con terminazione null nel buffer *lpszMsg.* Il messaggio verrà troncato a *cbMsgMax* meno il carattere di terminazione null dalla funzione **ConfigDriver** se è maggiore o uguale a *cbMsgMax* caratteri.
