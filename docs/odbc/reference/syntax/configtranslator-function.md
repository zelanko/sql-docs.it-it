---
title: Funzione ConfigTranslator | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306032"
---
# <a name="configtranslator-function"></a>Funzione ConfigTranslator
**Conformità**  
 Versione introdotta: ODBC 2,0  
  
 **Riepilogo**  
 **ConfigTranslator** restituisce un'opzione di conversione predefinita per un convertitore. Può trovarsi nella DLL di conversione o in una DLL di installazione separata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndParent*  
 Input Handle della finestra padre. Se l'handle è null, nella funzione non verrà visualizzata alcuna finestra di dialogo.  
  
 *pvOption*  
 Output Opzione di conversione a 32 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigTranslator** restituisce false, un valore * \*pfErrorCode* associato viene inserito nel buffer di errore del programma di installazione mediante una chiamata a **SQLPostInstallerError** e può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i * \*valori pfErrorCode* che possono essere restituiti da **SQLInstallerError** e ne illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido o è null.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o del convertitore|Errore specifico del driver per il quale non è stato definito alcun errore del programma di installazione ODBC. L'argomento *SzError* in una chiamata alla funzione **SQLPostInstallerError** deve contenere il messaggio di errore specifico del driver.|  
|ODBC_ERROR_INVALID_OPTION|Opzione di conversione non valida|L'argomento *pvOption* contiene un valore non valido.|  
  
## <a name="comments"></a>Commenti  
 Se il traduttore supporta solo una singola opzione di conversione, **ConfigTranslator** restituisce true e imposta *pvOption* sull'opzione a 32 bit. In caso contrario, determina l'opzione di conversione predefinita da usare. **ConfigTranslator** può visualizzare una finestra di dialogo con cui un utente seleziona un'opzione di conversione predefinita.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di un'opzione di conversione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selezione di un convertitore|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Impostazione di un'opzione di traduzione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
