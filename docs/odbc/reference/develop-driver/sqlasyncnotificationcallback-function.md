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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78764e1dccb7118d43cc967f3b03838366d6eb0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224515"
---
# <a name="sqlasyncnotificationcallback-function"></a>Funzione SQLAsyncNotificationCallback
**Conformità**  
 Versione introdotta: ODBC 3.8  
  
 Conformità agli standard: None  
  
 **Riepilogo**  
 **SQLAsyncNotificationCallback** consente al driver di richiamata da Gestione Driver quando si verifica un stato di avanzamento dell'operazione asincrona corrente dopo il driver restituisce SQL_STILL_EXECUTING. **SQLAsyncNotificationCallback** può solo chiamato dal driver.  
  
 I driver non chiamano **SQLAsyncNotificationCallback** con il nome di funzione **SQLAsyncNotificationCallback**. Al contrario, gestione Driver passa un puntatore a funzione a un driver come valore dell'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK per l'handle di connessione corrispondente o un handle di istruzione, rispettivamente. È possibile assegnare gli handle di diversi valori di puntatore funzione diversa. Il tipo del puntatore a funzione è definito come SQL_ASYNC_NOTIFICATION_CALLBACK.  
  
 **SQLAsyncNotificationCallback** è thread-safe. Un driver è possibile scegliere di usare più thread che chiamano **SQLAsyncNotificationCallback** su diversi gestisce contemporaneamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pContex*  
 Puntatore a una struttura di dati definita da Gestione Driver. Il valore viene passato al driver tramite SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) o SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT).  Il driver non ha accesso al valore.  
  
 *fLast*  
 Utilizzato da un driver per indica che la chiamata di funzione di callback è quello più recente per l'operazione asincrona corrente. Quando Gestione Driver chiama la funzione anche in questo caso, il driver restituirà un codice restituito diverso da SQL_STILL_EXECUTING. Gestione Driver può utilizzare queste informazioni, ad esempio, per informare in anticipo l'applicazione che verrà completata l'operazione asincrona.  
  
 Se *gestiscono* non è un handle valido del tipo specificato da *HandleType*, **SQLCancelHandle** non restituisca SQL_INVALID_HANDLE.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnostica  
 **SQLAsyncNotificationCallback** restituisce SQL_ERROR per due situazioni seguenti (queste informazioni indicano un problema di implementazione nel driver o gestione Driver.  
  
|Errore|Descrizione|  
|-----------|-----------------|  
|Connessione o l'istruzione non ha richiesto la notifica.||  
|Non è valido *gestire*|Il driver passato un handle non valido, quali i test di convalida interno di gestione Driver non è riuscita.|  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione asincrona (metodo di polling)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
