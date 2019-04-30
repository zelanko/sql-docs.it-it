---
title: Funzione ConfigDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d69db144a460bb2f662c8ba906bf0302cdf98388
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232074"
---
# <a name="configdriver-function"></a>Funzione ConfigDriver
**Conformità**  
 Versione introdotta: ODBC 2.5  
  
 **Riepilogo**  
 **ConfigDriver** consente di eseguire l'installazione e disinstallazione funzioni senza richiedere il programma per chiamare un programma di installazione **ConfigDSN**. Questa funzione eseguirà funzioni specifiche del driver, ad esempio la creazione di informazioni di sistema specifici del driver e conversioni DSN durante l'installazione, nonché pulitura delle modifiche del sistema di informazioni durante la disinstallazione. Questa funzione viene esposta tramite la DLL di installazione driver o una DLL di installazione separato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
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
 *hwndParent*  
 [Input] Handle della finestra padre. Se l'handle è null, la funzione non verrà visualizzata alcuna finestra di dialogo.  
  
 *fRequest*  
 [Input] Tipo di richiesta. Il *trattano* argomento deve essere uno dei valori seguenti:  
  
 ODBC_INSTALL_DRIVER: Installare un nuovo driver.  
  
 ODBC_REMOVE_DRIVER: Rimuovere un driver.  
  
 Questa opzione può anche essere specifici del driver, nel qual caso il *trattano* argomento per la prima opzione deve iniziare da ODBC_CONFIG_DRIVER_MAX + 1. Il *trattano* argomento per qualsiasi altra opzione è necessario anche avviare da un valore maggiore ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Input] Il nome del driver come registrato nella chiave Odbcinst. ini di informazioni di sistema.  
  
 *lpszArgs*  
 [Input] Una stringa con terminazione null che contiene gli argomenti per una specifica del driver *trattano*.  
  
 *lpszMsg*  
 [Output] Una stringa con terminazione null che contiene un messaggio di output dal programma di installazione di driver.  
  
 *cbMsgMax*  
 [Input] Lunghezza di *lpszMsg*.  
  
 *pcbMsgOut*  
 [Output] Numero totale di byte disponibili per restituire *lpszMsg*.  
  
 Se il numero di byte disponibili da restituire è maggiore o uguale a *cbMsgMax*, il messaggio di output in *lpszMsg* verrà troncato *cbMsgMax* meno la terminazione di tipo null carattere. Il *pcbMsgOut* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigDriver** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore viene inserito nel buffer di errore di programma di installazione da una chiamata al **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento non è valido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> L'opzione di specifica del driver era minore o uguale a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido. Non trovato nel Registro di sistema.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|Non è stato possibile eseguire l'operazione richiesta per il *trattano* argomento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o Microsoft translator|Un errore specifico del driver per cui non si verificano errori di programma di installazione ODBC definita. Il *SzError* argomento in una chiamata per il **SQLPostInstallerError** (funzione) deve contenere il messaggio di errore specifico del driver.|  
  
## <a name="comments"></a>Commenti  
  
### <a name="driver-specific-options"></a>Opzioni specifiche del driver  
 Un'applicazione può richiedere funzionalità specifiche del driver esposte dal driver tramite il *trattano* argomento. Il *trattano* per la prima opzione verrà ODBC_CONFIG_DRIVER_MAX più 1, e le opzioni aggiuntive verranno incrementate di 1 da tale valore. Eventuali argomenti richiesti dal driver per tale funzione deve essere fornita in una stringa con terminazione null passato il *lpszArgs* argomento. I driver che fornisce questa funzionalità è necessario gestire una tabella delle opzioni specifiche del driver. Le opzioni devono essere completamente documentate nella documentazione del driver. Gli autori di applicazioni che usano le opzioni specifiche del driver devono essere consapevoli che in questo modo l'applicazione meno interoperativa.  
  
### <a name="messages"></a>Messaggi  
 Una routine di installazione di driver può inviare un messaggio di testo a un'applicazione sotto forma di stringa con terminazione null nel *lpszMsg* buffer. Il messaggio verrà troncato a *cbMsgMax* meno il carattere di terminazione null per il **ConfigDriver** funzione se è maggiore o uguale a *cbMsgMax* caratteri.
