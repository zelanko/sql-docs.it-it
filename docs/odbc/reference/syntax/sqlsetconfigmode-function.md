---
title: Funzione SQLSetConfigMode . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293281"
---
# <a name="sqlsetconfigmode-function"></a>Funzione SQLSetConfigMode
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLSetConfigMode** imposta la modalità di configurazione che indica dove si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>Argomenti  
 *WConfigMode (Modalità di base)*  
 [Ingresso] La modalità di configurazione del programma di installazione (vedere "Commenti"). Il valore in wConfigMode può essere:The value in *wConfigMode* can be:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLSetConfigMode** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non valida|L'argomento *wConfigMode* non contiene ODBC_USER_DSN, ODBC_SYSTEM_DSN o ODBC_BOTH_DSN.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene utilizzata per impostare la posizione in cui si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema. Se *wConfigMode* è ODBC_USER_DSN, il DSN è un DSN utente e la funzione legge dalla voce Odbc.ini in HKEY_CURRENT_USER. Se è ODBC_SYSTEM_DSN, il DSN è un DSN di sistema e la funzione legge dalla voce Odbc.ini in HKEY_LOCAL_MACHINE. Se è ODBC_BOTH_DSN, HKEY_CURRENT_USER viene provato e, in caso di errore, viene utilizzato HKEY_LOCAL_MACHINE.  
  
 Questa funzione non influisce su **SQLCreateDataSource** e **SQLDriverConnect**. La modalità di configurazione deve essere impostata quando un driver legge dal Registro di sistema chiamando **SQLGetPrivateProfileString** o scrive nel Registro di sistema chiamando **SQLWritePrivateProfileString**. Le chiamate a **SQLGetPrivateProfileString** e **SQLWritePrivateProfileString** utilizzano la modalità di configurazione per sapere su quale parte del Registro di sistema operare.  
  
> [!CAUTION]  
>  **SQLSetConfigMode** deve essere chiamato solo quando necessario; se la modalità non è impostata correttamente, il programma di installazione ODBC potrebbe non funzionare correttamente.  
  
 **SQLSetConfigMode** apporta una modifica diretta del Registro di sistema della modalità di configurazione. Ciò è distinto dal processo di modifica della modalità di configurazione mediante una chiamata a **SQLConfigDataSource**. Una chiamata a **SQLConfigDataSource** imposta la modalità di configurazione per distinguere l'utente e DSN di sistema quando si modifica un DSN. Prima della restituzione, **SQLConfigDataSource** reimposta la modalità di configurazione su BOTHDSN.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Creazione di un'origine dati|[SQLCreateDataSource (origine SQLCreateDataSource)](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Recupero della modalità di configurazione|[MODALità SQLGetConfigSQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
