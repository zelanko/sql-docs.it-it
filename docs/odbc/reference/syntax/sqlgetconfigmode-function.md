---
title: Funzione SQLGetConfigMode . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc11bec24ede3352dd43f3645fb8c720b77fdabe
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285691"
---
# <a name="sqlgetconfigmode-function"></a>Funzione SQLGetConfigMode
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLGetConfigMode** recupera la modalità di configurazione che indica dove si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pwConfigMode (Modalità pwConfig)*  
 [Uscita] Puntatore al buffer contenente la modalità di configurazione. (Vedere "Commenti").") Il valore in * \*pwConfigMode* può essere:The value in pwConfigMode can be:  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetConfigMode** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Questa funzione viene utilizzata per determinare dove si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema. Se * \*pwConfigMode* è ODBC_USER_DSN, il DSN è un DSN utente e la funzione legge dalla voce Odbc.ini in HKEY_CURRENT_USER. Se è ODBC_SYSTEM_DSN, il DSN è un DSN di sistema e la funzione legge dalla voce Odbc.ini in HKEY_LOCAL_MACHINE. Se è ODBC_BOTH_DSN, HKEY_CURRENT_USER viene provato e, in caso di errore, viene utilizzato HKEY_LOCAL_MACHINE.  
  
 Per impostazione predefinita, **SQLGetConfigMode** restituisce ODBC_BOTH_DSN. Quando un DSN utente o un DSN di sistema viene creato da una chiamata a **SQLConfigDataSource**, la funzione imposta la modalità di configurazione per ODBC_USER_DSN o ODBC_SYSTEM_DSN per distinguere dSN utente e di sistema durante la modifica di un DSN. Prima della restituzione, **SQLConfigDataSource** reimposta la modalità di configurazione su ODBC_BOTH_DSN.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Impostazione della modalità di configurazione|[METODO SQLSetConfig](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
