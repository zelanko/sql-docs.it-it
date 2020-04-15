---
title: Notifica del completamento della funzione asincrona . Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287821"
---
# <a name="notification-of-asynchronous-function-completion"></a>Notifica del completamento di funzioni asincrone
In Windows 8 SDK, ODBC ha aggiunto un meccanismo per notificare alle applicazioni quando un'operazione asincrona viene completata, che verrà definita "notifica al completamento". Per altre informazioni, vedere [Esecuzione asincrona (metodo di notifica).](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md) In questo argomento vengono illustrati alcuni dei problemi per gli sviluppatori di driver.  
  
## <a name="the-interface-between-the-driver-manager-and-driver"></a>L'interfaccia tra Gestione driver e Driver  
 Gestione Driver fornisce internamente una funzione di callback [SQLAsyncNotificationCallback Function](../../../odbc/reference/develop-driver/sqlasyncnotificationcallback-function.md). **SQLAsyncNotificationCallback** può essere chiamato solo dal driver, ovvero un'applicazione non può chiamarlo direttamente. Il driver chiama **SQLAsyncNotificationCallback** ogni volta che vengono ricevuti nuovi dati dal server dopo la restituzione dell'ultima SQL_STILL_EXECUTING.  
  
 Gestione Driver fornisce un meccanismo di callback in modo che un driver può notificare a Gestione Driver quando sono stati fatti alcuni progressi nell'esecuzione di un'operazione asincrona dopo che la funzione corrispondente restituisce SQL_STILL_EXECUTING  
  
 Gestione Driver imposta l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK su un handle di connessione driver con un puntatore a funzione non NULL, che è di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, per il driver di lavorare in modalità di notifica per tutte le operazioni asincrone su tale handle. Analogamente, Gestione Driver imposta il SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK attributo su un handle di istruzione driver con un puntatore a funzione non NULL, che è anche di tipo SQL_ASYNC_NOTIFICATION_CALLBACK, per il driver di lavorare in modalità di notifica per tutte le operazioni asincrone su tale handle.  
  
 Se viene eseguita un'operazione asincrona su un handle del driver, le funzioni del driver asincrono devono funzionare in uno stile non bloccante. Se l'operazione non può essere completata immediatamente, la funzione del driver deve restituire SQL_STILL_EXECUTING. Questo requisito è vero sia per la modalità di polling che per la modalità di notifica.  
  
 Se un handle è in modalità asincrona di notifica, il driver deve chiamare la funzione di callback di notifica, il cui indirizzo è il valore per l'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK, una volta dopo la restituzione di SQL_STILL_EXECUTING. In altre parole, un SQL_STILL_EXECUTING restituito deve essere associato a una chiamata della funzione di callback di notifica. Il driver deve utilizzare il valore corrente dell'attributo SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT o SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT handle come valore per il parametro della funzione di chiamata *pContext*.  
  
 Il driver non deve richiamare nel thread che chiama la funzione del driver; non vi è alcun motivo per notificare lo stato di avanzamento prima che la funzione venga restituita. Il driver deve utilizzare il proprio thread per il callback. Gestione Driver non utilizzerà il thread di callback del driver per l'esecuzione di logica di elaborazione estesa.  
  
 Gestione Driver chiamerà nuovamente la funzione originale dopo che il driver richiama. Gestione Driver può utilizzare un thread che non è né un thread dell'applicazione né un thread del driver. Se il driver utilizza alcune informazioni associate al thread (ad esempio, token di sicurezza o identificatore utente), il driver deve salvare le informazioni necessarie nella chiamata asincrona iniziale e utilizzare il valore salvato prima del completamento dell'intera operazione asincrona. In genere, solo **SQLDriverConnect**, **SQLConnect**o **SQLBrowseConnect** devono utilizzare questo tipo di informazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
