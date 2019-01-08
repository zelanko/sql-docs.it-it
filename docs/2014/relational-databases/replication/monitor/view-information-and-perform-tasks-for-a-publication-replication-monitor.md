---
title: Visualizzare le informazioni ed eseguire attività per una pubblicazione (Monitoraggio replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 148ad2ba9ad0fb6575b787b992744666010fd3e1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781203"
---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>Visualizzare le informazioni ed eseguire attività per una pubblicazione (Monitoraggio replica)
  In Monitoraggio replica sono disponibili le schede seguenti che includono le informazioni sulla pubblicazione selezionata:  
  
-   **Tutte le sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Agenti**  
  
     In questa scheda vengono visualizzate informazioni su tutti gli agenti utilizzati da una pubblicazione:  
  
    -   Agente snapshot, utilizzato da tutte le pubblicazioni.  
  
    -   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.  
  
    -   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali contenenti sottoscrizioni ad aggiornamento in coda.  
  
-   **Avvisi** (per server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive)  
  
    -   Questa scheda consente di specificare avvisi per gli agenti.  
  
-   **Token di traccia** (solo replica transazionale, per server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive).  
  
     Questa scheda consente di misurare la latenza, ovvero l'intervallo di tempo che intercorre tra il commit di una transazione nel server di pubblicazione e il commit della transazione corrispondente nel Sottoscrittore.  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>Per visualizzare le informazioni ed eseguire le attività per una pubblicazione  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Per visualizzare e modificare le proprietà della pubblicazione, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Proprietà**.  
  
3.  Per visualizzare le informazioni sulle sottoscrizioni, fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
     Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una sottoscrizione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-subscription-agents.md).  
  
4.  Per visualizzare informazioni sugli agenti, fare clic sulla scheda **Agenti** . In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione &#40;Monitoraggio replica&#41;](view-information-and-perform-tasks-for-publication-agents.md).  
  
5.  Per visualizzare informazioni su avvisi e valore soglia dell'agente, fare clic sulla scheda **Avvisi** . Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Per visualizzare le informazioni sui token di traccia, fare clic sulla scheda **Token di traccia** . Per ulteriori informazioni sulle modalità di utilizzo dei token di traccia, vedere [Misurazione della latenza e convalida delle connessioni per la replica transazionale](measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md)   
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
