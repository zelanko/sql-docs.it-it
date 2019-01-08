---
title: Informazioni di pubblicazione, elenco verifica sottoscrizioni (pubblicazione transazionale, SQL Server 2005 e versioni successive) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.tran.f1
ms.assetid: 6bc64ddb-5c86-4681-a391-77fc1d3c4e6e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53a19b1de1c8aa0be89d0a743007b141bdb169b2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52766913"
---
# <a name="publisher-information-subscription-watch-list-transactional-publication-sql-server-2005-and-later"></a>Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni (Pubblicazione transazionale, SQL Server 2005 e versioni successive)
  La scheda **Elenco verifica sottoscrizioni** è disponibile per i server di distribuzione in cui viene eseguito SQL Server 2005 e versioni successive. Consente di visualizzare informazioni sulle sottoscrizioni da tutte le pubblicazioni disponibili nel server di pubblicazione selezionato. È possibile filtrare l'elenco delle sottoscrizioni per visualizzare errori, avvisi ed eventuali sottoscrizioni con prestazioni scarse. Questa scheda offre un'unica posizione per un amministratore di monitorare tutte le attività di replica nel server di pubblicazione: Monitoraggio replica Visualizza infatti tutte le sottoscrizioni che richiedono attenzione in base al tipo di replica selezionato e all'opzione scelta nel **mostrare** casella di riepilogo a discesa. Poiché gli elementi visualizzati in questa scheda si basano sullo stato e le prestazioni correnti, le sottoscrizioni vengono visualizzate in questa pagina solo se queste corrispondono all'opzione selezionata nella casella di riepilogo **Mostra** .  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni su una sottoscrizione e sulle attività correlate, fare clic con il pulsante destro del mouse sulla riga della sottoscrizione e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: Ordinare una o più colonne nella **Ordina colonne** nella finestra di dialogo.  
  
-   **Seleziona colonne da visualizzare**: Selezionare le colonne da visualizzare e l'ordine in cui si desidera visualizzarli nel **Scegli colonne** nella finestra di dialogo.  
  
-   **Filtro**: Filtrare le righe nella griglia in base ai valori di colonna il **impostazioni filtro** nella finestra di dialogo.  
  
-   **Cancella filtro**: Cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Mostra sottoscrizioni transazionali**  
 Consente di selezionare il tipo di sottoscrizioni (transazionali, snapshot o merge) da visualizzare per il server di distribuzione selezionato.  
  
 **Mostra**  
 Consente di selezionare gli stati della sottoscrizione da visualizzare per il tipo di sottoscrizione selezionato. Ad esempio, è possibile scegliere di visualizzare solo le sottoscrizioni con errori.  
  
 **Stato**  
 Stato di ogni sottoscrizione determinato dallo stato dell'agente di distribuzione o dell'agente di lettura log. Viene visualizzato lo stato con priorità più alta. Lo stato può inoltre essere determinato dall'agente di lettura coda nel caso in cui vengano utilizzate sottoscrizioni ad aggiornamento in coda.  
  
 Per impostazione predefinita, la griglia contenente le informazioni sulla sottoscrizione viene ordinata in base alla colonna **Stato** e quindi ordinata in base alla colonna **Prestazioni** per le sottoscrizioni che hanno lo stesso stato. Nell'elenco seguente vengono indicati i valori di stato possibili e l'ordinamento di tali valori, ad esempio gli errori vengono sempre visualizzati nella parte superiore della griglia.  
  
-   Errore  
  
-   Prestazioni critiche  
  
-   Scadenza imminente/Scaduta  
  
-   Sottoscrizione non inizializzata  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   In esecuzione  
  
 L'ordinamento determina inoltre il valore da visualizzare quando per una particolare sottoscrizione sono disponibili più stati. Se, ad esempio, per una sottoscrizione sono presenti errori e la scadenza della sottoscrizione è imminente, nella colonna **Stato** sarà visualizzato il valore **Errore**.  
  
 I valori di stato **Prestazioni critiche**, **Scadenza imminente/Scaduta**e **Sottoscrizione non inizializzata** sono avvisi. Quando viene visualizzato un avviso, nella colonna **Stato** viene inoltre visualizzato se è in esecuzione un agente. Ad esempio, lo stato potrebbe essere **In esecuzione, Prestazioni critiche**.  
  
 I valori di stato **Prestazioni critiche** e **Scadenza imminente/Scaduta** vengono visualizzati sono se sono stati impostati valori soglia. Per informazioni sulle misurazioni delle prestazioni e sull'impostazione dei valori soglia, vedere [Monitorare le prestazioni con Monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md) e [Impostare valori di soglia e avvisi in Monitoraggio replica](monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Sottoscrizione**  
 Il nome di ogni sottoscrizione, nel formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Pubblicazione**  
 Il nome della pubblicazione con cui viene sincronizzata una sottoscrizione, nel formato: *PublicationDatabaseName: PublicationName*.  
  
 **Prestazioni**  
 La valutazione delle prestazioni per ogni sottoscrizione è basata sulle misure più recenti rilevate da Monitoraggio replica e non riflette le prestazioni cronologiche. Le prestazioni vengono misurate per le sottoscrizioni delle pubblicazioni per le quali sono state definite soglie di prestazione. Se le soglie di prestazione non sono state definite per una pubblicazione, in questa colonna viene visualizzato **Non attivato**. La valutazione delle prestazioni può corrispondere a uno dei valori seguenti:  
  
-   Eccellenti  
  
-   Buone  
  
-   Discrete  
  
-   Scarse  
  
-   Critico  
  
 Se le prestazioni sono critiche, nella colonna **Stato** viene visualizzato **Prestazioni critiche** . Per altre informazioni sulla modalità con cui vengono definite le valutazioni delle prestazioni e impostati i valori soglia per le prestazione, vedere [Monitorare le prestazioni con Monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md).  
  
 **Latenza**  
 Tempo medio che intercorre tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore. La latenza visualizzata è basata sulle misure più recenti rilevate da Monitoraggio replica. Per altre informazioni sulla misurazione della latenza, vedere [Misurare la latenza e convalidare le connessioni per la replica transazionale](monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
 **Ultima sincronizzazione**  
 Data e ora dell'ultima esecuzione dell'agente di distribuzione. Se il processo di sincronizzazione è in corso, viene visualizzato **In corso** .  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Monitoraggio della replica](monitoring-replication.md)  
  
  
