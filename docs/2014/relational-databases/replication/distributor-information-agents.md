---
title: Informazioni sul database di distribuzione, Agenti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.Distributor.commonjobs..f1
ms.assetid: 5d601a64-6af0-42f9-81b1-cf0087f1c50d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc21cb1e775bcaeeea2d54718024b03a557864ae
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752223"
---
# <a name="distributor-information-agents"></a>Informazioni sul server di distribuzione, Agenti
  Nella scheda **Agenti** vengono visualizzate le informazioni sugli agenti e sui processi di manutenzione associati al server di pubblicazione e al Sottoscrittore.  
  
 Tra gli agenti disponibili nella scheda **Agenti** per un server di distribuzione nella vista Server di distribuzione sono inclusi tutti gli agenti disponibili nella scheda **Agenti** per un server di pubblicazione. Tuttavia, in **tale scheda** sono inclusi anche un agente del server di distribuzione e un agente di merge.  
  
 Per ulteriori informazioni sugli agenti snapshot, di lettura log, di lettura coda nonché sui processi di manutenzione, vedere [Publisher Information, Agents](publisher-information-agents.md). Si noti che quando si visualizzano le informazioni sugli agenti nella scheda **Agenti** per un server di distribuzione, le informazioni sul server di pubblicazione sono disponibili per gli agenti snapshot e di lettura log. Tuttavia, nella scheda **Agenti** per un server di distribuzione nella vista Server di distribuzione è possibile selezionare anche **Agente del server di distribuzione** e **Agente di merge**.  
  
## <a name="options"></a>Opzioni  
 Nelle sezioni seguenti sono descritti i dati visualizzati in questa scheda per l'agente del server di distribuzione e per quello di merge.  
  
### <a name="distributor-agent"></a>Agente del server di distribuzione  
 **Stato**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Non in esecuzione  
  
-   Mai avviato  
  
 **Server di pubblicazione**  
 Istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di pubblicazione.  
  
 **Pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Sottoscrizione**  
 Nome della sottoscrizione nel formato [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo di replica: push, pull o anonima.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Durata dell'esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e il tempo totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit dei comandi di inizializzazione nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **Latenza**  
 Tempo, espresso in secondi, trascorso tra il commit della modifica più recente nel database di pubblicazione e il commit del comando corrispondente nel database di distribuzione.  
  
 **N. transazioni**  
 Numero di transazioni di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **N. comandi**  
 Numero di comandi di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente. Un comando è equivalente a una modifica dei dati, ad esempio un aggiornamento.  
  
 **Media n. comandi**  
 Numero medio di comandi per transazione durante la più recente esecuzione dell'agente.  
  
### <a name="merge-agent"></a>Agente di merge  
 **Stato**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Riprova  
  
-   In esecuzione  
  
-   Non in esecuzione  
  
-   Mai avviato  
  
 **Server di pubblicazione**  
 Istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di pubblicazione.  
  
 **Pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Sottoscrizione**  
 Nome della sottoscrizione nel formato [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo di replica: push, pull o anonima.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Durata dell'esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e il tempo totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit delle modifiche nel database di distribuzione.  
  
 **Inserimenti del server di pubblicazione**  
 Numero di comandi INSERT applicati nel server di pubblicazione.  
  
 **Aggiornamenti del server di pubblicazione**  
 Numero di comandi UPDATE applicati nel server di pubblicazione.  
  
 **Eliminazioni del server di pubblicazione**  
 Numero di comandi DELETE applicati nel server di pubblicazione.  
  
 **Conflitti del server di pubblicazione**  
 Numero di conflitti che si verificano nel server di pubblicazione durante il processo di merge.  
  
 **Inserimenti del Sottoscrittore**  
 Numero di comandi INSERT applicati nel Sottoscrittore.  
  
 **Aggiornamenti del Sottoscrittore**  
 Numero di comandi UPDATE applicati nel Sottoscrittore.  
  
 **Eliminazioni del Sottoscrittore**  
 Numero di comandi DELETE applicati nel Sottoscrittore.  
  
 **Conflitti del Sottoscrittore**  
 Numero di conflitti che si verificano nel Sottoscrittore durante il processo di merge.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative agli agenti associati a una pubblicazione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [Monitoraggio della replica](monitoring-replication.md)  
  
  
