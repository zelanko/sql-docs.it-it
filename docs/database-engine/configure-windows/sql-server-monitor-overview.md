---
title: Panoramica di Monitoraggio SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a6f5e2b2bcd92c0a17ccada2ca755cbc14b9d647
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032496"
---
# <a name="sql-server-monitor-overview"></a>Panoramica di Monitoraggio SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In Monitoraggio SQL Server non sono disponibili funzioni di monitoraggio, ma moduli che consentono di effettuare tale operazione. Nei moduli di Monitoraggio SQL Server sono inclusi Monitoraggio replica e Monitoraggio mirroring del database.  
  
 Per usare uno di questi moduli, selezionarlo dal menu **Go** . Il modulo attualmente selezionato controlla il contenuto dei riquadri di navigazione e dei dettagli, l'interazione dell'utente nei riquadri dei dettagli e le query relative a contenuto e stato.  
  
> [!NOTE]  
>  Per altre informazioni su questi monitoraggi, vedere [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md) e [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
## <a name="permissions"></a>Autorizzazioni  
  
-   Monitoraggio replica  
  
     Per monitorare la replica, è necessaria l'assegnazione al ruolo predefinito del server **sysadmin** per il server di distribuzione o l'assegnazione al ruolo predefinito del database **replmonitor** nel database di distribuzione. Un amministratore di sistema può aggiungere qualsiasi utente al ruolo **replmonitor** , consentendo a tale utente di visualizzare l'attività di replica in Monitoraggio replica, ma non di amministrare la replica.  
  
-   Monitoraggio mirroring del database  
  
     Per monitorare il mirroring del database, è necessaria l'assegnazione al ruolo predefinito del server **sysadmin** o l'assegnazione al ruolo predefinito del database **dbm_monitor** nell'istanza del server. Se l'utente è membro di **sysadmin** o di **dbm_monitor** in una sola delle istanze del server partner, il monitoraggio può connettersi solo a tale partner e non è in grado di recuperare informazioni dall'altro partner. Per altre informazioni, vedere [Panoramica di Monitoraggio mirroring del database](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="menu-options"></a>Opzioni di menu  
 Monitoraggio SQL Server ha un menu che include comandi relativi a Monitoraggio SQL Server stesso. Il menu può inoltre includere comandi relativi al modulo selezionato.  
  
 Le opzioni di menu seguenti sono relative a Monitoraggio SQL Server.  
  
 **File**  
 Questo menu include il comando **Esci** .  
  
 **Azione**  
 Include il menu di scelta rapida del nodo selezionato nell'albero di navigazione.  
  
 **Go**  
 Include un elenco dei componenti di monitoraggio:  
  
-   Mirroring del database  
  
-   Replica  
  
 **Per utilizzare SQL Server Management Studio per il monitoraggio del mirroring del database**  
  
-   [Avviare il monitoraggio mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio del mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
