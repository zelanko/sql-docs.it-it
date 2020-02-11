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
ms.openlocfilehash: 0d5e0a10b8c530494fa3c026be0d36fde066a97c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053676"
---
# <a name="sqlpostinstallererror-function"></a>Funzione SQLPostInstallerError
**Conformità**  
 Versione introdotta: ODBC 3,0  
  
 **Summary**  
 **SQLPostInstallerError** fornisce un meccanismo per la libreria di installazione di un driver o di un convertitore per segnalare gli errori per le funzioni **ConfigDriver**, **ConfigDSN**e **ConfigTranslator** alla coda degli errori del programma di installazione. Le applicazioni non usano questa API; usano **SQLInstallerError** per recuperare l'errore.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *fErrorCode*  
 Input Codice di errore del programma di installazione.  
  
 *szErrorMsg*  
 Input Testo del messaggio di errore.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLPostInstallerError** non pubblica i valori di errore per se stesso. Se l'errore è stato inserito correttamente nella coda degli errori del programma di installazione (recuperabile con **SQLInstallerError**), viene restituito SQL_SUCCESS. Se il valore nell'argomento *dwErrorCode* non è uno dei codici di errore del programma di installazione specificato, verrà restituito SQL_ERROR.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Aggiunta, modifica o rimozione di origini dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Impostazione di un'opzione di traduzione|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
