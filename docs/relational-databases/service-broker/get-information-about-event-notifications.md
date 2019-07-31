---
title: Recuperare informazioni sulle notifiche degli eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fefdced57d611d241dbb96b71a0b220139683243
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083829"
---
# <a name="get-information-about-event-notifications"></a>Recupero di informazioni sulle notifiche degli eventi
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le viste del catalogo seguenti sono disponibili per eseguire query sui metadati relative alle notifiche degli eventi.  
  
 **Per ottenere informazioni relative alle notifiche degli eventi non a livello di server**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Per visualizzare i metadati relativi a eventuali notifiche degli eventi in **sys.event_notifications** creati a livello di database, è necessario disporre almeno dei seguenti elementi: Autorizzazione CONTROL, ALTER, TAKE OWNERSHIP o VIEW DEFINITION per il database, essere il proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY DATABASE EVENT NOTIFICATION. Per le notifiche degli eventi create in una coda specifica, è necessario disporre almeno di quanto segue: Autorizzazione CONTROL, ALTER, TAKE OWNERSHIP o VIEW DEFINITION per l'oggetto, essere il proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY DATABASE EVENT NOTIFICATION.  
  
 **Per ottenere informazioni relative alle notifiche degli eventi a livello di server**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  A livello minimo è necessario disporre di quanto segue: Autorizzazione CONTROL o VIEW ANY DEFINITION sul server, disporre di accesso o essere il proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY EVENT NOTIFICATION per visualizzare i metadati relativi a eventuali notifiche degli eventi in **sys.server_event_notifications**.  
  
 **Per ottenere informazioni relative a tutti gli eventi che possono attivare notifiche degli eventi**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Questa vista del catalogo non restituisce gruppi di eventi.  
  
## <a name="see-also"></a>Vedere anche  
 [Notifiche degli eventi](../../relational-databases/service-broker/event-notifications.md)  
  
  
