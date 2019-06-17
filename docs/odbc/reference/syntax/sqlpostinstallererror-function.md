---
title: Funzione SQLPostInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac7fb545938a0ec5f212e9c0da867fbea5db4817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536619"
---
# <a name="sqlpostinstallererror-function"></a>Funzione SQLPostInstallerError
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLPostInstallerError** fornisce un meccanismo per una libreria di programma di installazione driver o Microsoft translator per segnalare gli errori per il **ConfigDriver**, **ConfigDSN**, e **ConfigTranslator**  funzioni nella coda degli errori di programma di installazione. Applicazioni non usano questa API. usano **SQLInstallerError** per recuperare l'errore.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *fErrorCode*  
 [Input] Codice di errore di programma di installazione.  
  
 *szErrorMsg*  
 [Input] Testo del messaggio di errore.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLPostInstallerError** non registra i valori di errore per se stesso. Se l'errore è stato correttamente inserito nella coda degli errori di programma di installazione (recuperabili mediante **SQLInstallerError**), viene restituito SQL_SUCCESS. Verrà restituito SQL_ERROR se il valore di *dwErrorCode* argomento non è uno dei codici di errore di programma di installazione specificato.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Aggiunta, modifica o rimozione di origini dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Impostazione di un'opzione di conversione|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
