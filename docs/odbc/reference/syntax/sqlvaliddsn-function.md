---
title: Funzione SQLValidDSN | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbd8df72bcb0e76c8abcc3d738c2ff8da61a7bfe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039479"
---
# <a name="sqlvaliddsn-function"></a>Funzione SQLValidDSN
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLValidDSN** controlla la lunghezza e la validità del nome dell'origine dati prima che il nome viene aggiunto per le informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDSN*  
 [Input] Nome da controllare dell'origine dati.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se il nome dell'origine dati è valido. Restituisce FALSE se il nome dell'origine dati non è valido o la chiamata di funzione non è riuscita.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLValidDSN** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. Oggetto  *\*pfErrorCode* se viene restituito solo se la chiamata di funzione ha esito negativo, non è stato restituito FALSE perché il nome dell'origine dati non è valido. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLValidDSN** viene chiamato da un driver [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) per controllare la lunghezza del nome dell'origine dati e la validità dei singoli caratteri nel nome dell'origine dati. Controlla se la lunghezza del nome è maggiore di SQL_MAX_DSN_LENGTH, come definito in Sqlext. h. (La lunghezza del nome dell'origine dati è anche di verificarlo [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md).) **SQLValidDSN** controlla se uno qualsiasi dei seguenti caratteri non validi vengono inclusi nel nome dell'origine dati:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (nel programma di installazione DLL)|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|La scrittura di un nome dell'origine dati per le informazioni di sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
