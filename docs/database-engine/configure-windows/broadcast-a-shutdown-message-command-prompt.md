---
title: Trasmettere un messaggio di chiusura (prompt dei comandi) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 7517264d6ebc7baef2f066654f0309219f31b34d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786897"
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>Trasmissione di un messaggio di chiusura (prompt dei comandi)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questo argomento illustra come trasmettere un messaggio di arresto in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando il comando **net send** . Specificare nel messaggio l'orario di arresto dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , in modo da consentire agli utenti di completare le attività in corso.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>Per trasmettere un messaggio di arresto  
  
1.  Dal prompt dei comandi digitare quanto segue:  
  
     **net send /users "messaggio"**  
  
     L'opzione **/users** specifica che il messaggio verrà inviato a tutti gli utenti connessi al server  
  
> [!NOTE]  
>  Per usare il comando **net send** è necessario che sia in esecuzione il servizio Messenger sia sul computer che invia il messaggio sia sui computer che dovranno riceverlo. In Windows Server 2003 il servizio Messenger è disabilitato per impostazione predefinita. Per informazioni sul comando **net send**, vedere la documentazione di Windows.  
  
 In alcune reti potrebbe essere più appropriato contattare gli utenti per posta elettronica o telefonicamente. Utilizzare Monitor attività per determinare quali utenti sono attualmente connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni su Monitoraggio attività, vedere [Monitoraggio attività](../../relational-databases/performance-monitor/activity-monitor.md) e [Aprire Monitoraggio attività &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
