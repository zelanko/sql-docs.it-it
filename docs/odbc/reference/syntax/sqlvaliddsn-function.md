---
title: 'Funzione SQLValidDSN : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286971"
---
# <a name="sqlvaliddsn-function"></a>Funzione SQLValidDSN
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLValidDSN** controlla la lunghezza e la validità del nome dell'origine dati prima che il nome venga aggiunto alle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDSN*  
 [Ingresso] Nome dell'origine dati da verificare.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se il nome dell'origine dati è valido. Restituisce FALSE se il nome dell'origine dati non è valido o la chiamata di funzione non è riuscita.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLValidDSN** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Un * \*pfErrorCode* viene restituito solo se la chiamata di funzione non è riuscita, non se FALSE è stato restituito perché il nome dell'origine dati non è valido. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLValidDSN** viene chiamato dal [configDSN](../../../odbc/reference/syntax/configdsn-function.md) di un driver per controllare la lunghezza del nome dell'origine dati e la validità dei singoli caratteri nel nome dell'origine dati. Controlla se la lunghezza del nome è maggiore di SQL_MAX_DSN_LENGTH, come definito in Sqlext.h. La lunghezza del nome dell'origine dati viene controllata anche da [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md). **SQLValidDSN** controlla se uno dei seguenti caratteri non validi sono inclusi nel nome dell'origine dati:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (nella DLL di installazione)|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Scrittura di un nome di origine dati nelle informazioni di sistemaWriting a data source name to the system information|[Istruzione SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
