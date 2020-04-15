---
title: Funzione SQLPostInstallerError . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdceff5c4e175ba9f135c6e5e4405933b1a86b7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306892"
---
# <a name="sqlpostinstallererror-function"></a>Funzione SQLPostInstallerError
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLPostInstallerError** fornisce un meccanismo per un driver o un traduttore libreria di installazione per segnalare gli errori per le funzioni **ConfigDriver**, **ConfigDSN**e **ConfigTranslator** alla coda degli errori del programma di installazione. Le applicazioni non utilizzano questa API; utilizzano **SQLInstallerError** per recuperare l'errore.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *FErrorCode (Codice errore)*  
 [Ingresso] Codice di errore del programma di installazione.  
  
 *Szerrormsg*  
 [Ingresso] Testo del messaggio di errore.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLPostInstallerError** non registra i valori di errore per se stesso. Se l'errore è stato inviato correttamente nella coda degli errori del programma di installazione (recuperabile utilizzando **SQLInstallerError**), viene restituito SQL_SUCCESS. SQL_ERROR verrà restituito se il valore nell'argomento *dwErrorCode* non è uno dei codici di errore del programma di installazione specificato.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver (Driver di Configurazione)](../../../odbc/reference/syntax/configdriver-function.md)|  
|Aggiunta, modifica o rimozione di origini dati|[ConfigDSN (informazioni in locale)](../../../odbc/reference/syntax/configdsn-function.md)|  
|Impostazione di un'opzione di traduzione|[Traduttore di configurazione](../../../odbc/reference/syntax/configtranslator-function.md)|
