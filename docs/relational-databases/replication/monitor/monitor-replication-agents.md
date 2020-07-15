---
title: Monitorare gli agenti di replica | Microsoft Docs
description: Monitoraggio replica di SQL Server offre una visualizzazione a livello di sistema dell'attività di replica e consente di trovare informazioni su un agente specifico.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7984491281088f345e3e263356c6dad323d2cf5a
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807605"
---
# <a name="monitor-replication-agents"></a>Monitoraggio degli agenti di replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Monitoraggio replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre una visualizzazione a livello di sistema dell'attività di replica e semplifica l'individuazione di informazioni su un agente specifico. Nell'elenco seguente vengono inclusi tutti gli agenti, le relative schede di Monitoraggio replica e un collegamento all'argomento in cui si spiega come accedere a queste schede:  
  
-   Gli agenti seguenti sono associati alle pubblicazioni in Monitoraggio replica:  
  
    -   agente snapshot  
  
    -   Agente di lettura log  
  
    -   Agente di lettura coda  
  
     Accedere a informazioni e attività associate a questi agenti tramite le schede seguenti: **Agenti** (disponibile per ogni server di pubblicazione e pubblicazione) e **Avvisi** (disponibile per ogni pubblicazione). Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Gli agenti seguenti sono associati alle sottoscrizioni in Monitoraggio replica:  
  
    -   Agente di distribuzione  
  
    -   Agente di merge  
  
     Accedere a informazioni e attività associate a questi agenti tramite le schede seguenti: **Elenco verifica sottoscrizioni** (disponibile per ogni server di pubblicazione) o **Tutte le sottoscrizioni** (disponibile per ogni pubblicazione). Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>Utilizzo di SQL Server Management Studio per il monitoraggio degli agenti di replica  
 In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] sono disponibili le finestre di dialogo seguenti per il monitoraggio degli agenti di replica:  
  
-   **Visualizza stato agente snapshot** (per tutte le pubblicazioni)  
  
-   **Visualizza stato agente di lettura log** (per tutte le pubblicazioni transazionali)  
  
-   **Visualizza stato sincronizzazione** (per tutte le sottoscrizioni: questa finestra di dialogo consente l'accesso all'agente di distribuzione e all'agente di merge)  
  
 Monitoraggio replica offre informazioni aggiuntive su ogni agente e consente di monitorare l'agente di lettura coda, se utilizzato. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>Per monitorare l'agente snapshot e l'agente di lettura log  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse su una pubblicazione e quindi scegliere **Visualizza stato agente di lettura log** o **Visualizza stato agente snapshot**.  
  
4.  Nella finestra di dialogo **Visualizza stato agente di lettura log** o **Visualizza stato agente snapshot** :  
  
    -   Visualizzare lo stato dell'agente.  
  
    -   Avviare o arrestare l'agente se necessario.  
  
    -   Fare clic su **Esegui monitoraggio** per avviare **Monitoraggio replica**.  
  
5.  Fare clic su **Close**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>Per monitorare l'agente di distribuzione e l'agente di merge (dal server di pubblicazione)  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Espandere la pubblicazione della sottoscrizione da monitorare.  
  
4.  Fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza stato sincronizzazione**.  
  
5.  Nella finestra di dialogo **Visualizza stato sincronizzazione** :  
  
    -   Visualizzare lo stato dell'agente.  
  
    -   Avviare o arrestare l'agente se necessario.  
  
    -   Per le sottoscrizioni push fare clic su **Esegui monitoraggio** per avviare **Monitoraggio replica**.  
  
    -   Per le sottoscrizioni pull fare clic su **Visualizza cronologia processi** per avviare **Visualizzatore file log**e visualizzare l'output del log dell'agente.  
  
6.  Fare clic su **Close**.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>Per monitorare l'agente di distribuzione e l'agente di merge (dal Sottoscrittore)  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Sottoscrizioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione che si desidera monitorare e quindi scegliere **Visualizza stato sincronizzazione**.  
  
4.  Nella finestra di dialogo **Visualizza stato sincronizzazione** :  
  
    -   Visualizzare lo stato dell'agente.  
  
    -   Avviare o arrestare l'agente se necessario.  
  
    -   Fare clic su **Visualizza cronologia processi** per avviare **Visualizzatore file log**e visualizzare l'output del log dell'agente.  
  
5.  Fare clic su **Close**.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica degli agenti di replica](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
