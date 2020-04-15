---
title: Funzione ConfigTranslator . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306032"
---
# <a name="configtranslator-function"></a>Funzione ConfigTranslator
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **ConfigTranslator** restituisce un'opzione di conversione predefinita per un traduttore. Può essere nella DLL del traduttore o in una DLL di installazione separata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndPadre*  
 [Ingresso] Handle della finestra padre. La funzione non visualizzerà alcuna finestra di dialogo se l'handle è null.  
  
 *pvOption (Opzione)*  
 [Uscita] Un'opzione di conversione a 32 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigTranslator** restituisce FALSE, un valore * \*pfErrorCode* associato viene inviato al buffer degli errori del programma di installazione da una chiamata a **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido o NULL.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o del traduttore|Errore specifico del driver per il quale non è presente alcun errore definito del programma di installazione ODBC. *L'argomento SzError* in una chiamata alla funzione **SQLPostInstallerError** deve contenere il messaggio di errore specifico del driver.|  
|ODBC_ERROR_INVALID_OPTION|Opzione di conversione non valida|L'argomento *pvOption* contiene un valore non valido.|  
  
## <a name="comments"></a>Commenti  
 Se il traduttore supporta una sola opzione di conversione, **ConfigTranslator** restituisce TRUE e imposta *pvOption* sull'opzione a 32 bit. In caso contrario, determina l'opzione di conversione predefinita da utilizzare. **ConfigTranslator** può visualizzare una finestra di dialogo con cui un utente seleziona un'opzione di conversione predefinita.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Ottenere un'opzione di traduzione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selezione di un traduttore|[SQLGetTranslator (Traduttore)](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Impostazione di un'opzione di traduzione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
