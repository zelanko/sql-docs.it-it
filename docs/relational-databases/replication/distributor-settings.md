---
title: Impostazioni del server di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 506ae386a49a8a1485dc1e062ba58d264a7b7921
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76284037"
---
# <a name="distributor-settings"></a>Impostazioni del server di distribuzione
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La finestra di dialogo **Impostazioni del server di distribuzione** consente di modificare le impostazioni dei server di distribuzione aggiunti al riquadro sinistro di Monitoraggio replica.  
  
## <a name="options"></a>Opzioni  
 **Connetti automaticamente all'avvio di Monitoraggio replica**  
 Selezionare questa opzione per consentire la connessione di Monitoraggio replica al server di distribuzione e per recuperare informazioni sullo stato.  
  
 **Connection**  
 Fare clic su questa opzione per visualizzare la finestra di dialogo **Connetti al server** . In questo modo sarà possibile visualizzare e modificare le proprietà e le credenziali di connessione utilizzate da Monitoraggio replica per la connessione al server di distribuzione.  
  
 **Aggiorna automaticamente lo stato del server di distribuzione e delle sue pubblicazioni**  
 Selezionare questa opzione per consentire l'aggiornamento automatico dello stato del server di distribuzione da parte di Monitoraggio replica. Se questa opzione è selezionata, tramite Monitoraggio replica viene eseguito il polling del server di distribuzione per ottenere informazioni sullo stato in base all'intervallo di polling impostato utilizzando l'opzione **Frequenza di aggiornamento** . Per ulteriori informazioni sull'aggiornamento in Monitoraggio replica, vedere [Caching, Refresh, and Replication Monitor Performance](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frequenza di aggiornamento**  
 Immettere un valore, espresso in secondi, per specificare la frequenza di polling del server di distribuzione per ottenere informazioni sullo stato da parte di Monitoraggio replica. Valori inferiori comportano polling più frequenti. Questa condizione può influire sulle prestazioni nel server di distribuzione qualora si stiano monitorando molti server di pubblicazione. È consigliabile eseguire prove sul sistema per determinare un valore appropriato. L'impostazione **Frequenza di aggiornamento** viene utilizzata anche se si seleziona **Aggiornamento automatico** in una delle finestre dei dettagli di Monitoraggio replica.  
  
 **Mostra tutti i server di pubblicazione di questo server di distribuzione nel gruppo seguente**  
 Selezionare un gruppo di server di pubblicazione nell'elenco. Il server di pubblicazione viene visualizzato in questo gruppo nel riquadro sinistro. I gruppi consentono di organizzare i server di pubblicazione e non influiscono sul funzionamento della replica.  
  
 **Nuovo gruppo**  
 Fare clic su questa opzione per creare un nuovo gruppo di server di pubblicazione. Un gruppo di server di pubblicazione consente di organizzare facilmente i server di pubblicazione all'interno di Monitoraggio replica. I gruppi non influiscono sulla replica dei dati o sulla relazione tra i server in una topologia di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
