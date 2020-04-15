---
title: Funzione SQLCompleteAsync . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299656"
---
# <a name="sqlcompleteasync-function"></a>Funzione SQLCompleteAsync
**Conformità**  
 Versione introdotta: ODBC 3.8  
  
 Conformità agli standard: Nessuno  
  
 **Riepilogo**  
 **SQLCompleteAsync** può essere utilizzato per determinare quando una funzione asincrona viene completata usando l'elaborazione basata su notifiche o polling. Per ulteriori informazioni sulle operazioni asincrone, vedere [esecuzione asincrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** viene implementato solo in Gestione driver ODBC.  
  
 Nella modalità di elaborazione asincrona basata sulla notifica, **SQLCompleteAsync** deve essere chiamato dopo che Gestione Driver genera l'oggetto evento utilizzato per la notifica. **SQLCompleteAsync** completa l'elaborazione asincrona e la funzione asincrona genererà un codice restituito.  
  
 Nella modalità di elaborazione asincrona basata sul polling, **SQLCompleteAsync** è un'alternativa alla chiamata della funzione asincrona originale, senza dover specificare gli argomenti nella chiamata di funzione asincrona originale. **SQLCompleteAsync** può essere utilizzato indipendentemente dall'abilitazione della libreria di cursori ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 [Ingresso] Tipo dell'handle in base al quale completare l'elaborazione asincrona. I valori validi sono SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Ingresso] Handle in base al quale completare l'elaborazione asincrona. Se *Handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** restituisce SQL_INVALID_HANDLE.  
  
 Se *Handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** restituisce SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Uscita] Puntatore a un buffer che conterrà il codice restituito dell'API asincrona. Se *AsyncRetCodePtr* è NULL, **SQLCompleteAsync** restituisce SQL_ERROR.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Se **SQLCompleteAsync** restituisce SQL_SUCCESS, un'applicazione deve ottenere il codice restituito della funzione asincrona dal buffer a cui punta *AsyncRetCodePtr*. L'oggetto SQLSTATE associato, se presente, può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un handle di istruzione o un *HandleType* di SQL_HANDLE_DBC e un handle di connessione. Tali record di diagnostica sono associati alla funzione asincrona, non a questa funzione **SQLCompleteAsync.Those diagnostic** records are associated with the asynchronous function, not this SQLCompleteAsync function.  
  
 **SQLCompleteAsync** restituisce un codice diverso da SQL_SUCCESS per indicare che **SQLCompleteAsync** non viene chiamato correttamente. **SQLCompleteAsync** non pubblicherà alcun record di diagnostica in questo caso. I possibili codici di ritorno sono:  
  
-   SQL_INVALID_HANDLE: l'handle indicato da *HandleType* e *Handle* non è un handle valido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* è NULL o l'elaborazione asincrona non è abilitata sull'handle.  
  
-   SQL_NO_DATA: in modalità di notifica, non è in corso un'operazione asincrona o Gestione Driver non ha notificato l'applicazione. In modalità di polling, un'operazione asincrona non è in corso.  
  
## <a name="comments"></a>Commenti  
 In modalità di elaborazione asincrona basata sul polling, *AsyncRetCodePtr* potrebbe essere SQL_STILL_EXECUTING quando **SQLCompleteAsync** restituisce SQL_SUCCESS. L'applicazione deve continuare il polling fino a quando *AsyncRetCodePtr* non viene SQL_STILL_EXECUTING. Nella modalità di elaborazione asincrona basata sulle notifiche, *AsyncRetCodePtr* non verrà mai SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
