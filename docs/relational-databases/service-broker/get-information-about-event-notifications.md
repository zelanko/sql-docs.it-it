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
ms.openlocfilehash: d82126c304a40cfba88201f71b8073a815a169cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764959"
---
# <a name="get-information-about-event-notifications"></a>Recupero di informazioni sulle notifiche degli eventi
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Le viste del catalogo seguenti sono disponibili per eseguire query sui metadati relative alle notifiche degli eventi.  
  
 **Per ottenere informazioni relative alle notifiche degli eventi non a livello di server**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Per visualizzare i metadati relativi a notifiche degli eventi in **sys.event_notifications** creati a livello del database, è almeno necessario disporre dell'autorizzazione CONTROL, ALTER, TAKE OWNERSHIP oppure VIEW DEFINITION sul database, essere proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY DATABASE EVENT NOTIFICATION. Per le notifiche degli eventi create in una coda specifica, è almeno necessario disporre dell'autorizzazione CONTROL, ALTER, TAKE OWNERSHIP oppure VIEW DEFINITION sull'oggetto, essere proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY DATABASE EVENT NOTIFICATION.  
  
 **Per ottenere informazioni relative alle notifiche degli eventi a livello di server**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  È almeno necessario disporre dell'autorizzazione CONTROL o VIEW ANY DEFINITION sul server, essere dotati di accesso o essere il proprietario della notifica degli eventi oppure disporre dell'autorizzazione ALTER ANY EVENT NOTIFICATION per visualizzare i metadati relativi a eventuali notifiche degli eventi in **sys.server_event_notifications**.  
  
 **Per ottenere informazioni relative a tutti gli eventi che possono attivare notifiche degli eventi**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Questa vista del catalogo non restituisce gruppi di eventi.  
  
## <a name="see-also"></a>Vedere anche  
 [Notifiche degli eventi](../../relational-databases/service-broker/event-notifications.md)  
  
  
