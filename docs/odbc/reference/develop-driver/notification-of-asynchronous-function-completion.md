---
title: Notifica del completamento di funzione asincrona | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c54e545bdbd1ae137c24f79c71b53502480cbca9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690531"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notifica del completamento di funzioni asincrone
In Windows 8 SDK, ODBC aggiunto un meccanismo per notificare alle applicazioni quando viene completata un'operazione asincrona, che si farà riferimento a come "notifica di completamento". (Vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) per altre informazioni.) In questo argomento vengono descritti alcuni dei problemi per gli sviluppatori di driver.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>L'interfaccia tra il gestore dei Driver e il Driver  
 Gestione Driver offre internamente una funzione di richiamata [funzione SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** può essere chiamato solo dal driver, un'applicazione non è possibile chiamare direttamente. Il driver chiama **SQLAsyncNotificationCallback** ogni volta che i nuovi dati ricevuti dal server dopo l'ultima restituzione SQL_STILL_EXECUTING.  
  
 Gestione Driver fornisce un meccanismo di callback in modo che un driver può inviare una notifica in Gestione Driver quando alcuni lo stato di avanzamento è stata eseguita durante l'esecuzione di un'operazione asincrona dopo la funzione corrispondente restituisce SQL_STILL_EXECUTING  
  
 Gestione Driver consente di attivare un handle di connessione del driver con un puntatore a funzione non NULL, che è di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, per il driver in modalità di notifica per l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK qualsiasi asincrona operazioni su tale handle. Analogamente, gestione Driver imposta l'attributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK su un handle di istruzione di driver con un puntatore a funzione non NULL, che è anche di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, per il driver in modalità di notifica per operazioni asincrone in tale handle.  
  
 Se un'operazione asincrona viene eseguita su un handle di driver, le funzioni asincrone driver dovrebbero funzionare in uno stile non bloccante. Se l'operazione non è possibile completare immediatamente, la funzione driver deve restituire SQL_STILL_EXECUTING. Questo requisito vale per la modalità di notifica sia in modalità di polling.  
  
 Se in modalità asincrona di notifica è un handle, il driver deve chiamare la funzione di callback di notifica, il cui indirizzo è il valore dell'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una volta dopo restituzione SQL_STILL_EXECUTING. SQL_STILL_EXECUTING che restituiscono uno in altre parole, deve essere abbinato a una singola chiamata di funzione di callback di notifica. Il driver deve utilizzare il valore corrente dell'attributo handle SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT come valore per il parametro di chiamata di funzione di richiamata *pContext*.  
  
 Il driver non deve chiamare nuovamente nel thread che chiama la funzione di driver. non c'è nessun motivo per notificare lo stato di avanzamento prima che la funzione restituisce. Il driver deve utilizzare il proprio thread al callback. Gestione Driver non userà i thread di callback del driver per l'esecuzione di logica di elaborazione estesa.  
  
 The Driver Manager chiamerà la funzione originale nuovamente dopo che il driver chiama nuovamente. Gestione Driver può usare un thread diverso da un thread dell'applicazione o un thread di driver. Se il driver Usa alcune informazioni associate al thread (ad esempio, utente o token ID di sicurezza), il driver deve salvare le informazioni necessarie nella chiamata iniziale asincrona e usare il valore salvato prima dell'operazione asincrona completamente completa. In genere, solo **SQLDriverConnect**, **SQLConnect**, o **SQLBrowseConnect** è necessario utilizzare tale tipo di informazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
