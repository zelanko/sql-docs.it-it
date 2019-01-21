---
title: Finestra di dialogo "Impostazioni server di pubblicazione" di replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 24def3d19d38356bb48886a64a0566254aeb1aec
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132561"
---
# <a name="sql-server-replication-publisher-settings-dialog-box"></a>Finestra di dialogo "Impostazioni server di pubblicazione" di replica di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Impostazioni server di pubblicazione** consente di modificare le impostazioni per i server di pubblicazione aggiunti al riquadro sinistro di Monitoraggio replica.  
  
## <a name="options"></a>Opzioni  
 **Connessione server di pubblicazione**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Connetti al server** , che consente di visualizzare e modificare le proprietà e le credenziali di connessione utilizzate da Monitoraggio replica per la connessione a un server di pubblicazione.  
  
 **Connessione server di distribuzione**  
 Questa opzione viene visualizzata solo se il server di pubblicazione utilizza un server di distribuzione remoto. Fare clic su questo pulsante per visualizzare la finestra di dialogo **Connetti al server** , che consente di visualizzare e modificare le proprietà e le credenziali di connessione utilizzate da Monitoraggio replica per la connessione al server di distribuzione remoto.  
  
 **Connetti automaticamente all'avvio di Monitoraggio replica**  
 Selezionare questa casella di controllo per consentire a Monitoraggio replica di connettersi automaticamente al server di distribuzione e di recuperare informazioni sullo stato del server di pubblicazione selezionato nella griglia posta nella parte superiore della finestra di dialogo. Se questa casella di controllo è deselezionata è necessario connettersi manualmente dopo l'avvio di Monitoraggio replica. Fare clic con il pulsante destro del mouse sul server di pubblicazione visualizzato nel riquadro sinistro di Monitoraggio replica e scegliere **Connetti**.  
  
 **Aggiorna automaticamente lo stato del server di pubblicazione e delle sue pubblicazioni**  
 Selezionare questa opzione per consentire a Monitoraggio replica di aggiornare automaticamente lo stato del server di pubblicazione selezionato nella griglia posta nella parte superiore della finestra di dialogo. Se questa opzione è selezionata, Monitoraggio replica esegue il polling del server di distribuzione per ottenere informazioni sullo stato del server di pubblicazione e delle relative pubblicazioni. L'intervallo di polling viene impostato dall'opzione **Frequenza di aggiornamento** . Per altre informazioni sull'aggiornamento in Monitoraggio replica, vedere [Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frequenza di aggiornamento**  
 Immettere un valore, espresso in secondi, per specificare la frequenza di polling del server di distribuzione per ottenere informazioni sullo stato da parte di Monitoraggio replica. Valori inferiori indicano un polling più frequente, che influisce sulle prestazioni del server di distribuzione se il monitoraggio include un numero elevato di server di pubblicazione. È consigliabile eseguire prove sul sistema per determinare un valore appropriato. L'impostazione **Frequenza di aggiornamento** viene utilizzata anche se si seleziona **Aggiornamento automatico** in una delle finestre dei dettagli di Monitoraggio replica.  
  
 **Mostra server di pubblicazione nel gruppo seguente**  
 Selezionare un gruppo di server di pubblicazione nell'elenco. Il server di pubblicazione viene visualizzato in questo gruppo nel riquadro sinistro. I gruppi consentono di organizzare i server di pubblicazione e non influiscono sul funzionamento della replica.  
  
 **Nuovo gruppo**  
 Fare clic su questa opzione per creare un nuovo gruppo di server di pubblicazione. Un gruppo di server di pubblicazione consente di organizzare facilmente i server di pubblicazione all'interno di Monitoraggio replica. I gruppi non influiscono sulla replica dei dati o sulla relazione tra i server in una topologia di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
