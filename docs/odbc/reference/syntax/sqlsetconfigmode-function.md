---
title: Funzione SQLSetConfigMode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a10ec8f8fa6ef2b0e310680f58252f98628ff045
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215610"
---
# <a name="sqlsetconfigmode-function"></a>Funzione SQLSetConfigMode
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLSetConfigMode** imposta la modalità di configurazione che indica se la voce ini Elenca i valori DSN è nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argomenti  
 *wConfigMode*  
 [Input] La modalità di configurazione del programma di installazione (vedere "Commenti"). Il valore in *wConfigMode* può essere:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetConfigMode** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non validi|Il *wConfigMode* argomento non conteneva ODBC_USER_DSN, ODBC_SYSTEM_DSN o ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene utilizzata per impostare in cui la voce ini Elenca i valori DSN è nelle informazioni di sistema. Se *wConfigMode* è ODBC_USER_DSN, il DSN è un DSN utente e la funzione legge dalla voce ini in HKEY_CURRENT_USER. Se si tratta ODBC_SYSTEM_DSN, il DSN è un DSN di sistema e la funzione legge dalla voce ini in HKEY_LOCAL_MACHINE. Se si tratta ODBC_BOTH_DSN, viene eseguito un tentativo di HKEY_CURRENT_USER e in caso contrario, viene utilizzato HKEY_LOCAL_MACHINE.  
  
 Questa funzione non influisce **SQLCreateDataSource** e **SQLDriverConnect**. La modalità di configurazione deve essere impostata quando un driver legge il Registro di sistema chiamando **SQLGetPrivateProfileString** o la scrittura nel Registro di sistema chiamando **SQLWritePrivateProfileString**. Le chiamate a **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** usare la modalità di configurazione per sapere quale parte del Registro di sistema su cui operare.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve essere chiamato solo quando necessario; se la modalità è impostata in modo non corretto, il programma di installazione ODBC potrebbe non riuscire funzionare correttamente.  
  
 **SQLSetConfigMode** apporta una modifica diretta del Registro di sistema della modalità di configurazione. Si tratta di oltre il processo di modifica la modalità di configurazione da una chiamata a **SQLConfigDataSource**. Una chiamata a **SQLConfigDataSource** imposta la modalità di configurazione per distinguere i DSN di sistema e utente quando si modifica un DSN. Prima della restituzione, **SQLConfigDataSource** BOTHDSN Reimposta la modalità di configurazione.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Creazione di un'origine dati|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recuperare la modalità di configurazione|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
