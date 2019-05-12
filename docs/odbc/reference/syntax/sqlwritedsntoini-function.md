---
title: SQLWriteDSNToIni Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a36be7a98a39cab8b9df428b8d4bd9a1d399a1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536785"
---
# <a name="sqlwritedsntoini-function"></a>Funzione SQLWriteDSNToIni
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLWriteDSNToIni** aggiunge un'origine dati per le informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDSN*  
 [Input] Nome dell'origine dati da aggiungere.  
  
 *lpszDriver*  
 [Input] Descrizione del driver (in genere il nome del sistema DBMS associati) presentato agli utenti anziché il nome del driver fisico.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLWriteDSNToIni** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_DSN|DSN valido|Il *lpszDSN* argomento è contenuta una stringa che non è valida per un DSN.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non è riuscita|Il programma di installazione non è stato possibile creare un DSN nel Registro di sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLWriteDSNToIni** aggiunge l'origine dati alla sezione [ODBC Zdroje dat] le informazioni di sistema. Quindi crea una sezione specifica per l'origine dati e aggiunge una singola parola chiave (**Driver**) con il nome della DLL come relativo valore del driver. Se la sezione specifica di origine dati esiste già, **SQLWriteDSNToIni** rimuove la precedente sezione prima di creare quella nuova.  
  
 Il chiamante di questa funzione è necessario aggiungere tutte le parole chiave specifiche del driver e i valori per la sezione specifica origine dati le informazioni di sistema.  
  
 Se il nome dell'origine dati predefinita **SQLWriteDSNToIni** crea anche la sezione specifica di driver predefiniti nelle informazioni di sistema.  
  
 Questa funzione deve essere chiamata solo da una DLL di installazione.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(nel programma di installazione DLL)|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Rimozione di un nome dell'origine dati dalle informazioni di sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
