---
title: Monitoraggio (replica) | Microsoft Docs
description: Informazioni sugli strumenti di monitoraggio usati per tenere traccia dell'attività e dello stato della replica nella topologia di replica di SQL Server.
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 2d9b58373aa64a2e2ee377acace142803b13ba51
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477832"
---
# <a name="monitoring-replication"></a>Monitoraggio (replica)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Il monitoraggio di una topologia di replica rappresenta un aspetto essenziale della distribuzione di una replica. Dato che l'attività di replica viene distribuita, è fondamentale monitorarne l'attività e lo stato su tutti i computer interessati. Con l'uso di vari strumenti di monitoraggio è possibile rispondere a domande comuni quali: 

-   Il sistema di replica funziona correttamente?
-   Quali sottoscrizioni sono lente?
-   Con quale ritardo viene eseguita la sottoscrizione transazionale?
-   In quanto tempo una transazione di cui è stato appena eseguito il commit raggiungerà un Sottoscrittore nella replica transazionale?
-   Per quale motivo la sottoscrizione di tipo merge è lenta?
-   Perché l'agente non è in esecuzione?  
  

Per monitorare la replica è possibile utilizzare gli strumenti seguenti:  
  
-   **Monitoraggio replica per SQL Server**: il più importante strumento per il monitoraggio della replica che offre una visualizzazione incentrata sul server di pubblicazione dell'intera attività di replica. Per altre informazioni, vedere [Monitoring Replication](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md). 
-   **SQL Server Management Studio**: offre l'accesso a Monitoraggio replica. Consente anche di visualizzare lo stato attuale e l'ultimo messaggio registrato dagli agenti seguenti e di avviare e arrestare ogni agente: agente di lettura log, agente di snapshot, agente di merge e agente di distribuzione. Per altre informazioni, vedere [Monitor Replication Agents](../../../relational-databases/replication/monitor/monitor-replication-agents.md).  
  
-   **Transact-SQL (T-SQL) e Replication Management Objects (RMO)** : entrambe le interfacce consentono di monitorare tutti i tipi di replica dal database di distribuzione. La replica di tipo merge consente inoltre di monitorare la replica dal Sottoscrittore.  
  
-   **Avvisi per gli eventi degli agenti di replica**: durante la replica sono disponibili diversi avvisi predefiniti per gli eventi degli agenti di replica. Se necessario, è anche possibile creare nuovi avvisi. Gli avvisi possono essere utilizzati per avviare una risposta automatica in seguito a un evento e/o per inviare notifiche all'amministratore. Per altre informazioni, vedere [Usare gli avvisi per gli eventi degli agenti di replica](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
-   **Monitoraggio di sistema**: può essere utile per monitorare le prestazioni della replica tramite vari contatori. Per altre informazioni, vedere [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  

## <a name="see-also"></a>Vedere anche  
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   

  
  
