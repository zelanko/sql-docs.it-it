---
title: Funzione SQLCompleteAsync | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 736867be33531a73c0ada66a3be0f1245f1c483a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537593"
---
# <a name="sqlcompleteasync-function"></a>Funzione SQLCompleteAsync
**Conformità**  
 Versione introdotta: ODBC 3.8  
  
 Conformità agli standard: None  
  
 **Riepilogo**  
 **SQLCompleteAsync** può essere utilizzato per determinare quando una funzione asincrona è stata completata usando entrambi l'elaborazione o polling dal basato sulla notifica. Per altre informazioni sulle operazioni asincrone, vedere [esecuzione asincrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** è implementata solo in Gestione Driver ODBC.  
  
 In modalità di elaborazione asincrona basato su notifica **SQLCompleteAsync** deve essere chiamato dopo che il servizio di gestione Driver genera l'oggetto evento utilizzato per la notifica. **SQLCompleteAsync** completamento asincrono di elaborazione e la funzione asincrona verrà generato un codice restituito.  
  
 In modalità di elaborazione asincrona basati su polling **SQLCompleteAsync** è un'alternativa alla chiamata di funzione asincrona originale, senza la necessità di specificare gli argomenti nella chiamata di funzione asincrona originale. **SQLCompleteAsync** può essere usata indipendentemente dal fatto che, se la libreria di cursori ODBC è abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Input] Il tipo dell'handle su cui completamento asincrono di elaborazione. I valori validi sono SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Input] L'handle sul quale completare asincrona di elaborazione. Se *gestiscono* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** non restituisca SQL_INVALID_HANDLE.  
  
 Se *gestiscono* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** non restituisca SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Output] Puntatore a un buffer che conterrà il codice restituito dell'API asincrona. Se *AsyncRetCodePtr* sia impostato su NULL **SQLCompleteAsync** restituisce SQL_ERROR.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Se **SQLCompleteAsync** restituisce SQL_SUCCESS, un'applicazione devono ottenere il codice restituito della funzione asincrona dal buffer a cui punta *AsyncRetCodePtr*. Il valore SQLSTATE associato, se presente, può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* SQL_HANDLE_STMT e un handle di istruzione o un *HandleType* di SQL _ HANDLE_DBC e un handle di connessione. Tali record di diagnostica associati con la funzione asincrona, non usare **SQLCompleteAsync** (funzione).  
  
 **SQLCompleteAsync** restituisce un codice diverso da SQL_SUCCESS per indicare che **SQLCompleteAsync** non viene chiamato in modo corretto. **SQLCompleteAsync** non verranno registrati tutti i record di diagnostica in questo caso. Codici restituiti possibili sono:  
  
-   SQL_INVALID_HANDLE: L'handle indicato dal *HandleType* e *gestire* non è un handle valido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* è NULL o l'elaborazione asincrona non è abilitata sull'handle.  
  
-   SQL_NO_DATA: In modalità di notifica, un'operazione asincrona non è in corso o gestione Driver non ha alcuna notifica all'applicazione. In modalità di polling, un'operazione asincrona non è in corso.  
  
## <a name="comments"></a>Commenti  
 In modalità di elaborazione asincrona basati su polling *AsyncRetCodePtr* potrebbe essere SQL_STILL_EXECUTING quando **SQLCompleteAsync** restituisce SQL_SUCCESS. Applicazione deve mantenere il polling finché *AsyncRetCodePtr* non SQL_STILL_EXECUTING. In modalità di elaborazione asincrona basato su notifica *AsyncRetCodePtr* non potranno mai essere SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
