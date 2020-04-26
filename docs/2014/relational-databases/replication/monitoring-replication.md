---
title: Monitoraggio della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e2b3441d98bc9226abce3a49fd28820df6ec99ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62666869"
---
# <a name="monitoring-replication"></a>Monitoraggio (replica)
  Il monitoraggio di una topologia di replica rappresenta un aspetto essenziale della distribuzione di una replica. Dato che l'attività di replica viene distribuita, è fondamentale monitorarne l'attività e lo stato su tutti i computer interessati. Per monitorare la replica è possibile utilizzare gli strumenti seguenti:  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)][!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] Monitoraggio replica  
  
     Monitoraggio replica è lo strumento principale per il monitoraggio della replica, caratterizzato da una vista dell'intera attività di replica con priorità al server di pubblicazione. Per ulteriori informazioni, vedere [monitoraggio delle prestazioni con monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md).  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] consente di accedere a Monitoraggio replica. Consente inoltre di visualizzare lo stato attuale e l'ultimo messaggio registrato dall'agente di lettura log, dall'agente snapshot, dall'agente di merge e dall'agente di distribuzione, con la possibilità di avviare e arrestare ognuno di loro. Per altre informazioni, vedere [Monitor Replication Agents](monitor/monitor-replication-agents.md).  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] e oggetti RMO (Replication Management Objects)  
  
     Entrambe le interfacce consentono di monitorare tutti i tipi di replica dal server di distribuzione. La replica di tipo merge consente inoltre di monitorare la replica dal Sottoscrittore.  
  
-   Avvisi per gli eventi degli agenti di replica  
  
     Durante la replica sono disponibili vari avvisi predefiniti per gli eventi degli agenti di replica. Se necessario, è inoltre possibile crearne di nuovi. Gli avvisi possono essere utilizzati per avviare una risposta automatica in seguito a un evento e/o per inviare notifiche all'amministratore. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](agents/use-alerts-for-replication-agent-events.md).  
  
-   Monitor di sistema  
  
     Questa opzione può essere utile per monitorare le prestazioni della replica tramite vari contatori. Per altre informazioni, vedere [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Domande frequenti sull'amministrazione della replica](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Procedure consigliate per l'amministrazione della replica](administration/best-practices-for-replication-administration.md)   

  
  
