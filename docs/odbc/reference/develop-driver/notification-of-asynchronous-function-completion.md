---
title: Notifica del completamento asincrono della funzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 336565da-4203-4745-bce2-4f011c08e357
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a453967f2ffdda4af2a44429737f700f4a994cf8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287821"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notifica del completamento di funzioni asincrone
In Windows 8 SDK, ODBC ha aggiunto un meccanismo per notificare alle applicazioni il completamento di un'operazione asincrona, a cui si fa riferimento come "notifica al completamento". Per ulteriori informazioni, vedere [esecuzione asincrona (metodo di notifica)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) . In questo argomento vengono illustrati alcuni dei problemi per gli sviluppatori di driver.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>Interfaccia tra Gestione driver e driver  
 Gestione driver fornisce internamente una funzione di callback [SQLAsyncNotificationCallback](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** può essere chiamato solo dal driver, che non può essere chiamato direttamente da un'applicazione. Il driver chiama **SQLAsyncNotificationCallback** ogni volta che vengono ricevuti nuovi dati dal server dopo l'ultimo ritorno SQL_STILL_EXECUTING.  
  
 Gestione driver fornisce un meccanismo di callback che consente a un driver di inviare una notifica a gestione driver quando si è verificato uno stato di avanzamento durante l'esecuzione di un'operazione asincrona dopo la restituzione della funzione corrispondente SQL_STILL_EXECUTING  
  
 Gestione driver imposta l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK su un handle di connessione driver con un puntatore a funzione non NULL, che è di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, per il funzionamento del driver in modalità di notifica per qualsiasi operazione asincrona su tale handle. Analogamente, gestione driver imposta l'attributo SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK in un handle di istruzione del driver con un puntatore a funzione non NULL, che è anche di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, affinché il driver funzioni in modalità di notifica per qualsiasi operazione asincrona su tale handle.  
  
 Se un'operazione asincrona viene eseguita su un handle di driver, le funzioni del driver asincrono dovrebbero funzionare in uno stile non bloccante. Se l'operazione non può essere completata immediatamente, la funzione driver deve restituire SQL_STILL_EXECUTING. Questo requisito è valido per la modalità di polling e la modalità di notifica.  
  
 Se un handle è in modalità asincrona di notifica, è necessario che il driver chiami la funzione di callback delle notifiche, il cui indirizzo è il valore per l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una volta dopo la restituzione di SQL_STILL_EXECUTING. In altre parole, una restituzione di SQL_STILL_EXECUTING deve essere abbinata a una chiamata della funzione di callback di notifica. Il driver deve usare il valore corrente del SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT attributo handle come valore per il parametro *pContext*della funzione di chiamata.  
  
 Il driver non deve richiamare il thread che chiama la funzione di driver; non esiste alcun motivo per notificare lo stato di avanzamento prima che la funzione restituisca. Il driver deve utilizzare il proprio thread per la richiamata. Gestione driver non utilizzerà il thread di callback del driver per l'esecuzione di una logica di elaborazione completa.  
  
 Gestione driver chiamerà nuovamente la funzione originale dopo che il driver ha richiamato. Gestione driver può utilizzare un thread che non è né un thread dell'applicazione né un thread del driver. Se il driver usa alcune informazioni associate al thread, ad esempio un token di sicurezza o un identificatore utente, il driver deve salvare le informazioni necessarie nella chiamata asincrona iniziale e usare il valore salvato prima del completamento dell'intera operazione asincrona. In genere, solo **SQLDriverConnect**, **SQLConnect**o **SQLBrowseConnect** devono usare questo tipo di informazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
