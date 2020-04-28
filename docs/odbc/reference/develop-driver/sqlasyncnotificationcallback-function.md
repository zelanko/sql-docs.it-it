---
title: Funzione SQLAsyncNotificationCallback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6c182c48b8e5ddb70204ddd3a94d9651f97595d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294538"
---
# <a name="sqlasyncnotificationcallback-function"></a>Funzione SQLAsyncNotificationCallback
**Conformità**  
 Versione introdotta: ODBC 3,8  
  
 Conformità agli standard: nessuna  
  
 **Riepilogo**  
 **SQLAsyncNotificationCallback** consente a un driver di richiamare Gestione driver quando ci sono alcuni progressi per l'operazione asincrona corrente dopo che il driver restituisce SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** può essere chiamato solo dal driver.  
  
 I driver non chiamano **SQLAsyncNotificationCallback** con il nome della funzione **SQLAsyncNotificationCallback**. Il gestore di driver passa invece un puntatore a funzione a un driver come valore per l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK dell'handle di connessione o dell'handle di istruzione corrispondente, rispettivamente. A diversi handle possono essere assegnati valori di puntatore a funzione diversi. Il tipo del puntatore a funzione è definito come SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** è thread-safe. Un driver può scegliere di usare più thread che chiamano **SQLAsyncNotificationCallback** su handle diversi simultaneamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pContex*  
 Puntatore a una struttura di dati definita da Gestione driver. Il valore viene passato al driver tramite SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) o SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  Il driver non ha accesso al valore.  
  
 *fLast*  
 Utilizzato da un driver per indicare che questa chiamata di funzione di callback è l'ultima per l'operazione asincrona corrente. Il driver restituisce un codice restituito diverso da SQL_STILL_EXECUTING quando Gestione driver chiama di nuovo la funzione. Gestione driver può utilizzare queste informazioni, ad esempio, per informare l'applicazione in anticipo che l'operazione asincrona verrà completata.  
  
 Se *handle* non è un handle valido del tipo specificato da *HandleType*, **SQLCancelHandle** restituisce SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLAsyncNotificationCallback** può restituire SQL_ERROR per le due situazioni seguenti, che indicano un problema di implementazione nel driver o nella gestione driver.  
  
|Errore|Descrizione|  
|-----------|-----------------|  
|La connessione o l'istruzione non ha richiesto la notifica.||  
|*Handle* non valido|Il driver ha passato un handle non valido, che non ha superato i test interni di convalida di gestione driver.|  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
