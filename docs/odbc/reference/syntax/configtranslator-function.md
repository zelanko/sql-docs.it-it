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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b56a5ebd0ad00e2c3abb87b72d2de8735245f99
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537980"
---
# <a name="configtranslator-function"></a>Funzione ConfigTranslator
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **ConfigTranslator** restituisce un'opzione di conversione predefinita per una funzione di conversione. Può essere translator DLL o una DLL di installazione separato.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndParent*  
 [Input] Handle della finestra padre. Se l'handle è null, la funzione non verrà visualizzata alcuna finestra di dialogo.  
  
 *pvOption*  
 [Output] Un'opzione di conversione a 32 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **ConfigTranslator** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore viene inserito nel buffer di errore di programma di installazione da una chiamata a **SQLPostInstallerError**e può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento era NULL o non valido.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Errore specifico del driver o Microsoft translator|Un errore specifico del driver per cui non si verificano errori di programma di installazione ODBC definita. Il *SzError* argomento in una chiamata per il **SQLPostInstallerError** (funzione) deve contenere il messaggio di errore specifico del driver.|  
|ODBC_ERROR_INVALID_OPTION|Opzione di conversione non è valido|Il *pvOption* argomento è presente un valore non valido.|  
  
## <a name="comments"></a>Commenti  
 Se il convertitore supporta solo un'opzione di sola traduzione **ConfigTranslator** restituisce TRUE e imposta *pvOption* all'opzione di 32 bit. In caso contrario, determina l'opzione di conversione predefinita da utilizzare. **ConfigTranslator** può visualizzare una finestra di dialogo con cui un utente seleziona un'opzione di conversione predefinita.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Recupero di un'opzione di conversione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selezione di una funzione di conversione|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Impostazione di un'opzione di conversione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
