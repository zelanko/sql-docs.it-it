---
title: Implementare notifiche degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c5b17b45b50634806c60e5064efc6ebd9d03f8b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68197753"
---
# <a name="implement-event-notifications"></a>Implementazione di notifiche degli eventi
  Per implementare una notifica degli eventi, è necessario prima creare un servizio di destinazione che riceverà le notifiche degli eventi.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] per le notifiche degli eventi che prevedono l'invio di messaggi a Service Broker su un server remoto. La sicurezza del dialogo deve essere configurata manualmente in base al modello di sicurezza avanzata.  
  
## <a name="creating-the-target-service"></a>Creazione del servizio di destinazione  
 Non è necessario creare un servizio di origine di [!INCLUDE[ssSB](../../includes/sssb-md.md)]perché [!INCLUDE[ssSB](../../includes/sssb-md.md)] include il tipo di messaggio e di contratto seguente specifico per le notifiche degli eventi:  
  
```  
https://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 Il servizio di destinazione che riceve le notifiche degli eventi deve rispettare il contratto esistente.  
  
 **Per creare un server di destinazione**:  
  
1.  Creare una coda per ricevere messaggi.  
  
    > [!NOTE]  
    >  La coda riceve il tipo di messaggio seguente: `https://schemas.microsoft.com/SQL/Notifications/QueryNotification`.  
  
2.  Creare un servizio nella coda che faccia riferimento al contratto per le notifiche degli eventi.  
  
3.  Creare una route nel servizio per definire l'indirizzo a cui verranno inviati i messaggi per il servizio tramite [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Per le notifiche dell'evento la cui destinazione è rappresentata da un servizio nello stesso database, specificare `ADDRESS = 'LOCAL'`.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] Il routing determina il servizio che riceve i messaggi di notifica. Se la destinazione della notifica degli eventi è rappresentata da un servizio in un server remoto, il server di origine e il server di destinazione dovranno entrambi disporre di route definite che assicurino la corretta comunicazione bidirezionale.  
  
 Nell'esempio seguente vengono creati una coda, un servizio nella coda e una route nel servizio per gestire i messaggi provenienti dal contratto per le notifiche degli eventi.  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[https://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## <a name="creating-the-event-notification"></a>Creazione della notifica degli eventi  
 Le notifiche degli eventi vengono create utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION e vengono eliminate utilizzando l'istruzione DROP EVENT NOTIFICATION. Per modificare la notifica di un evento, è necessario eliminarla e quindi ricrearla.  
  
 Nell'esempio seguente viene creata la notifica di evento `CreateDatabaseNotification`. Per ogni evento `CREATE_DATABASE` generato nel server, questa notifica invia un messaggio al servizio `NotifyService` creato in precedenza.  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  Le notifiche degli eventi riconoscono gli eventi CREATE_SCHEMA e le definizioni <schema_element> delle istruzioni CREATE SCHEMA come eventi distinti. Si supponga ad esempio di creare una notifica di evento in entrambi gli eventi CREATE_SCHEMA e CREATE_TABLE e di eseguire il batch seguente.  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  In questo caso la notifica dell'evento viene generata due volte, una prima volta quando viene generato l'evento CREATE_SCHEMA e una seconda volta quando viene generato l'evento CREATE_TABLE. È consigliabile non creare notifiche degli eventi sia negli eventi CREATE_SCHEMA che nel testo <schema_element> delle definizioni CREATE SCHEMA corrispondenti. In alternativa, compilare nell'applicazione la logica necessaria a evitare di acquisire dati per eventi non desiderati.  
  
 **Per creare la notifica di un evento**  
  
-   [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-notification-transact-sql)  
  
 **Per eliminare la notifica di un evento**  
  
-   [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-notification-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero di informazioni sulle notifiche degli eventi](event-notifications.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
