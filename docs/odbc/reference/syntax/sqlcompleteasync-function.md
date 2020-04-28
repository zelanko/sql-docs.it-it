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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299656"
---
# <a name="sqlcompleteasync-function"></a>Funzione SQLCompleteAsync
**Conformità**  
 Versione introdotta: ODBC 3,8  
  
 Conformità agli standard: nessuna  
  
 **Riepilogo**  
 È possibile utilizzare **SQLCompleteAsync** per determinare quando una funzione asincrona viene completata utilizzando l'elaborazione basata sulle notifiche o sul polling. Per ulteriori informazioni sulle operazioni asincrone, vedere [esecuzione asincrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** viene implementato solo in Gestione driver ODBC.  
  
 Nella modalità di elaborazione asincrona basata su notifiche, **SQLCompleteAsync** deve essere chiamato dopo che Gestione driver genera l'oggetto evento usato per la notifica. **SQLCompleteAsync** completa l'elaborazione asincrona e la funzione asincrona genererà un codice restituito.  
  
 In modalità di elaborazione asincrona basata sul polling, **SQLCompleteAsync** è un'alternativa alla chiamata della funzione asincrona originale, senza la necessità di specificare gli argomenti nella chiamata di funzione asincrona originale. **SQLCompleteAsync** può essere utilizzata indipendentemente dal fatto che la libreria di cursori ODBC sia abilitata.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *HandleType*  
 Input Tipo dell'handle su cui completare l'elaborazione asincrona. I valori validi sono SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 Input Handle su cui completare l'elaborazione asincrona. Se *handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** restituisce SQL_INVALID_HANDLE.  
  
 Se *handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCompleteAsync** restituisce SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 Output Puntatore a un buffer che conterrà il codice restituito dell'API asincrona. Se *AsyncRetCodePtr* è null, **SQLCompleteAsync** restituisce SQL_ERROR.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Se **SQLCompleteAsync** restituisce SQL_SUCCESS, un'applicazione deve ottenere il codice restituito della funzione asincrona dal buffer a cui punta *AsyncRetCodePtr*. Il valore SQLSTATE associato, se presente, può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_STMT e un handle di istruzione oppure un *HandleType* di SQL_HANDLE_DBC e un handle di connessione. Tali record di diagnostica sono associati alla funzione asincrona, non a questa funzione **SQLCompleteAsync** .  
  
 **SQLCompleteAsync** restituisce un codice diverso da SQL_SUCCESS per indicare che **SQLCompleteAsync** non è stato chiamato correttamente. In questo caso, **SQLCompleteAsync** non pubblicherà alcun record di diagnostica. I codici restituiti possibili sono:  
  
-   SQL_INVALID_HANDLE: l'handle indicato da *HandleType* e *handle* non è un handle valido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* è null o l'elaborazione asincrona non è abilitata nell'handle.  
  
-   SQL_NO_DATA: in modalità di notifica, un'operazione asincrona non è in corso o non è stata notificata all'applicazione da parte di gestione driver. In modalità di polling non è in corso un'operazione asincrona.  
  
## <a name="comments"></a>Commenti  
 In modalità di elaborazione asincrona basata sul polling, *AsyncRetCodePtr* potrebbe essere SQL_STILL_EXECUTING quando **SQLCompleteAsync** restituisce SQL_SUCCESS. L'applicazione deve continuare a eseguire il polling fino a quando *AsyncRetCodePtr* non è SQL_STILL_EXECUTING. Nella modalità di elaborazione asincrona basata su notifiche, *AsyncRetCodePtr* non verrà mai SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
