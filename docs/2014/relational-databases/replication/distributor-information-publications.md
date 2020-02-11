---
title: Replica di SQL Server finestra di dialogo "informazioni sul server di distribuzione" | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.Distributor.Publications.f1
- sql12.rep.monitor.Distributor.commonjobs..f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql12.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2d738066e4832c029743d53f7ec99dbb1b6fe5cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721363"
---
# <a name="distributor-information-dialog-box"></a>Finestra di dialogo informazioni server di distribuzione 
In questo argomento vengono fornite informazioni sulla finestra di dialogo **server di distribuzione** 

## <a name="publications"></a>Pubblicazioni

  Nella scheda **Pubblicazioni** vengono fornite informazioni di riepilogo relative a tutte le pubblicazioni nel server di distribuzione selezionato nel riquadro sinistro.  
  
### <a name="options"></a>Opzioni  
 Nelle informazioni visualizzate relative alle pubblicazioni supportate dal server di distribuzione è inclusa una colonna in cui è contenuta l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di pubblicazione. In caso contrario, le informazioni sulla pubblicazione corrispondono alle informazioni sulla pubblicazione fornite quando si visualizzano pubblicazioni nella vista Server di pubblicazione di Monitoraggio replica. Per ulteriori informazioni sulle colonne nella scheda **Pubblicazioni** , vedere [Publisher Information, Publications](publisher-information-publications.md).  

## <a name="subscription-watch-list"></a>Elenco verifica sottoscrizioni

### <a name="transactional-replication"></a>Replica transazionale 
  Nelle informazioni per le sottoscrizioni transazionali è incluso il nome del server di pubblicazione. In caso contrario, la funzionalità e le informazioni fornite in questa finestra di dialogo sono le stesse della vista Server di pubblicazione. Per altre informazioni su come usare questa finestra di dialogo, vedere [Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni &#40;pubblicazione transazionale, SQL Server 2005 e versioni successive&#41;](publisher-information-subscription-watch-list-transactional.md).  

### <a name="merge-replication"></a>Replica di tipo merge
  Nelle informazioni per le sottoscrizioni delle pubblicazioni di tipo merge è incluso il nome del server di pubblicazione. In caso contrario, la funzionalità e le informazioni fornite in questa finestra di dialogo sono le stesse della vista Server di pubblicazione. Per altre informazioni su come usare questa finestra di dialogo, vedere [Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni &#40;pubblicazione di tipo merge, SQL Server 2005 e versioni successive&#41;](publisher-information-subscription-watch-list-merge-publication.md). 

### <a name="snapshot-replication"></a>Replica snapshot
  Nelle informazioni per le sottoscrizioni delle pubblicazioni snapshot è incluso il nome del server di pubblicazione. In caso contrario, la funzionalità e le informazioni fornite in questa finestra di dialogo sono le stesse della vista Server di pubblicazione. Per altre informazioni su come usare questa finestra di dialogo, vedere [Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni &#40;pubblicazione snapshot, SQL Server 2005 e versioni successive&#41;](publisher-information-subscription-watch-list-snapshot.md).  

## <a name="agents"></a>Agenti
  Nella scheda **Agenti** vengono visualizzate le informazioni sugli agenti e sui processi di manutenzione associati al server di pubblicazione e al Sottoscrittore.  
  
 Tra gli agenti disponibili nella scheda **Agenti** per un server di distribuzione nella vista Server di distribuzione sono inclusi tutti gli agenti disponibili nella scheda **Agenti** per un server di pubblicazione. Tuttavia, in **tale scheda** sono inclusi anche un agente del server di distribuzione e un agente di merge.  
  
 Per ulteriori informazioni sugli agenti snapshot, di lettura log, di lettura coda nonché sui processi di manutenzione, vedere [Publisher Information, Agents](publisher-information-agents.md). Si noti che quando si visualizzano le informazioni sugli agenti nella scheda **Agenti** per un server di distribuzione, le informazioni sul server di pubblicazione sono disponibili per gli agenti snapshot e di lettura log. Tuttavia, nella scheda **Agenti** per un server di distribuzione nella vista Server di distribuzione è possibile selezionare anche **Agente del server di distribuzione** e **Agente di merge**.  
  
### <a name="options"></a>Opzioni  
 Nelle sezioni seguenti sono descritti i dati visualizzati in questa scheda per l'agente del server di distribuzione e per quello di merge.  
  
### <a name="distributor-agent"></a>Agente del server di distribuzione  
 **Status**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore    
-   Riprova    
-   In esecuzione    
-   Non in esecuzione    
-   Mai avviato  
  
 **Autore**  
 Istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di pubblicazione.  
  
 **Pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Sottoscrizione**  
 Nome della sottoscrizione nel formato [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo di replica: push, pull o anonima.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Duration**  
 Durata dell'esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e il tempo totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
 **Frequenza recapito**  
 Frequenza, in comandi al secondo, con cui viene eseguito il commit dei comandi di inizializzazione nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **Latency**  
 Tempo, espresso in secondi, trascorso tra il commit della modifica più recente nel database di pubblicazione e il commit del comando corrispondente nel database di distribuzione.  
  
 **N. transazioni**  
 Numero di transazioni di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente.  
  
 **N. comandi**  
 Numero di comandi di cui è stato eseguito il commit nel database di distribuzione durante la più recente esecuzione dell'agente. Un comando è equivalente a una modifica dei dati, ad esempio un aggiornamento.  
  
 **Media n. comandi**  
 Numero medio di comandi per transazione durante la più recente esecuzione dell'agente.  
  
### <a name="merge-agent"></a>Agente di merge  
 **Status**  
 Stato dell'agente. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore    
-   Riprova    
-   In esecuzione    
-   Non in esecuzione    
-   Mai avviato  
  
 **Autore**  
 Istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del server di pubblicazione.  
  
 **Pubblicazione**  
 Nome della pubblicazione a cui è associato l'agente.  
  
 **Sottoscrizione**  
 Nome della sottoscrizione nel formato [*SubscriberName*].[*Database*].  
  
 **Tipo**  
 Tipo di replica: push, pull o anonima.  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Duration**  
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
 [Monitoraggio della replica](monitoring-replication.md)  
  
  
