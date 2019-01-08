---
title: Monitoraggio della replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 81f596d2-27a5-489d-bf8d-0f4361decd02
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae9c89b3fa3d9392e27cce9199f7c1b1b8f31dee
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771423"
---
# <a name="monitoring-replication"></a>Monitoraggio della replica
  Monitoraggio replica di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è uno strumento grafico che consente di monitorare lo stato generale di una topologia di replica. Tale strumento offre informazioni dettagliate sullo stato e sulle prestazioni di pubblicazioni e sottoscrizioni, consentendo all'utente di rispondere a domande comuni quali:  
  
-   Il sistema di replica funziona correttamente?  
  
-   Quali sottoscrizioni sono lente?  
  
-   Con quale ritardo viene eseguita la sottoscrizione transazionale?  
  
-   In quanto tempo una transazione di cui è stato appena eseguito il commit raggiungerà un Sottoscrittore nella replica transazionale?  
  
-   Per quale motivo la sottoscrizione di tipo merge è lenta?  
  
-   Perché l'agente non è in esecuzione?  
  
 Per monitorare la replica, è necessario che un utente sia un membro del ruolo predefinito del server **sysadmin** nel server di distribuzione o un membro del ruolo predefinito del database **replmonitor** nel database di distribuzione. Un amministratore di sistema può aggiungere qualsiasi utente al ruolo **replmonitor** , consentendo a tale utente di visualizzare l'attività di replica in Monitoraggio replica, ma non di amministrare la replica.  
  
## <a name="in-this-section"></a>In questa sezione  
 Negli argomenti seguenti sono incluse informazioni sulle funzionalità di Monitoraggio replica.  
  
 [Panoramica dell'interfaccia di Monitoraggio replica](overview-of-the-replication-monitor-interface.md)  
 Vengono descritte tutte le finestre e le schede di Monitoraggio replica e sono incluse informazioni su come rispondere alle domande elencate in precedenza.  
  
 [Avviare Monitoraggio replica](start-the-replication-monitor.md)  
 Viene descritto come avviare Monitoraggio replica.  
  
 [Consentire a utenti non amministratori di usare Monitoraggio replica](allow-non-administrators-to-use-replication-monitor.md)  
 Viene descritto come assegnare autorizzazioni agli utenti non amministratore in modo che possano utilizzare Monitoraggio replica.  
  
 [Aggiungere e rimuovere server di pubblicazione da Monitoraggio replica](add-and-remove-publishers-from-replication-monitor.md)  
 Viene descritto come aggiungere o rimuovere server di pubblicazione da Monitoraggio replica.  
  
 [Aggiornare i dati in Monitoraggio replica](refresh-data-in-replication-monitor.md)  
 Viene descritto come aggiornare i dati in Monitoraggio replica.  
  
 [Monitorare le prestazioni con Monitoraggio replica](monitor-performance-with-replication-monitor.md)  
 Descrive come monitorare le prestazioni in Monitoraggio replica, incluse le informazioni sull'impostazione delle soglie di prestazione. Include informazioni sulle statistiche a livello di articolo per la replica di merge per ottenere una vista dettagliata dell'elaborazione.  
  
 [Misurazione della latenza e convalida delle connessioni per la replica transazionale](measure-latency-and-validate-connections-for-transactional-replication.md)  
 Descrive i token di traccia che consentono di misurare le prestazioni di una topologia di replica transazionale.  
  
 [Monitorare gli agenti di replica](../agents/replication-agents.md)  
 Descrive come reperire informazioni su ogni agente di replica.  
  
 [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)  
 Descrive gli avvisi e le soglie che è possibile impostare in Monitoraggio replica. È consigliabile abilitare gli avvisi per la topologia, in modo da poter essere informati tempestivamente sullo stato e sulle prestazioni.  
  
 [Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica](caching-refresh-and-replication-monitor-performance.md)  
 Descrive il modo in cui Monitoraggio replica memorizza dati e calcoli nella cache per migliorare le prestazioni e illustra la relazione tra l'aggiornamento dell'interfaccia utente e quello della cache.  
  
 [Visualizzare lo stato delle pubblicazioni e delle sottoscrizioni in Monitoraggio replica](view-publication-and-subscription-status-in-replication-monitor.md)  
 Viene descritto come visualizzare informazioni sullo stato di una Pubblicazione o Sottoscrizione tramite Monitoraggio replica.  
  
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
 Viene descritto come visualizzare le informazioni e come eseguire le attività per un server di pubblicazione tramite Monitoraggio replica  
  
 [Visualizzare le informazioni ed eseguire attività per una pubblicazione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  
 Viene descritto come visualizzare le informazioni e come eseguire le attività per una pubblicazione tramite Monitoraggio replica  
  
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-publication-agents.md)  
 Viene descritto come visualizzare le informazioni e come eseguire le attività per gli agenti associati a una pubblicazione tramite Monitoraggio replica.  
  
 [Visualizzare le informazioni ed eseguire attività relative a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
 Viene descritto come visualizzare le informazioni e come eseguire le attività per una Sottoscrizione tramite Monitoraggio replica  
  
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-subscription-agents.md)  
 Viene descritto come visualizzare le informazioni e come eseguire le attività per gli agenti associati a una Sottoscrizione tramite Monitoraggio replica.  
  
  
