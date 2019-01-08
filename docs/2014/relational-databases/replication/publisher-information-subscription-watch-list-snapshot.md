---
title: Informazioni di pubblicazione, elenco verifica sottoscrizioni (pubblicazione Snapshot, SQL Server 2005 e versioni successive) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1520e67a3aee6a7afdec7bcc7dfbe6d4e8ee81b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777543"
---
# <a name="publisher-information-subscription-watch-list-snapshot-publication-sql-server-2005-and-later"></a>Informazioni sul server di pubblicazione, Elenco verifica sottoscrizioni (Pubblicazione snapshot, SQL Server 2005 e versioni successive)
  La scheda **Elenco verifica sottoscrizioni** è disponibile per i server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive e consente di visualizzare le informazioni sulle sottoscrizioni da tutte le pubblicazioni disponibili nel server di pubblicazione selezionato. È possibile filtrare l'elenco delle sottoscrizioni per visualizzare errori, avvisi ed eventuali sottoscrizioni con prestazioni scarse. Questa scheda offre un'unica posizione per un amministratore di monitorare tutte le attività di replica nel server di pubblicazione: Monitoraggio replica Visualizza infatti tutte le sottoscrizioni che richiedono attenzione in base al tipo di replica selezionato e all'opzione scelta nel **mostrare** casella di riepilogo a discesa. Poiché gli elementi visualizzati in questa scheda si basano sullo stato e le prestazioni correnti, le sottoscrizioni vengono visualizzate in questa pagina solo se queste corrispondono all'opzione selezionata nella casella di riepilogo **Mostra** .  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni su una sottoscrizione e sulle attività correlate, fare clic con il pulsante destro del mouse sulla riga della sottoscrizione e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: Ordinare una o più colonne nella **Ordina colonne** nella finestra di dialogo.  
  
-   **Seleziona colonne da visualizzare**: Selezionare le colonne da visualizzare e l'ordine in cui si desidera visualizzarli nel **Scegli colonne** nella finestra di dialogo.  
  
-   **Filtro**: Filtrare le righe nella griglia in base ai valori di colonna il **impostazioni filtro** nella finestra di dialogo.  
  
-   **Cancella filtro**: Cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Mostra sottoscrizioni snapshot**  
 Consente di selezionare il tipo di sottoscrizioni (transazionali, snapshot o merge) da visualizzare per il server di distribuzione selezionato.  
  
 **Mostra**  
 Consente di selezionare gli stati della sottoscrizione da visualizzare per il tipo di sottoscrizione selezionato. Ad esempio, è possibile scegliere di visualizzare solo le sottoscrizioni con errori.  
  
 **Stato**  
 Stato di ogni sottoscrizione determinato dallo stato dell'agente snapshot o dell'agente di distribuzione. Viene visualizzato lo stato con priorità più alta.  
  
 Per impostazione predefinita, la griglia contenente le informazioni sulla sottoscrizione viene ordinata in base alla colonna **Stato** . Nell'elenco seguente vengono indicati i valori di stato possibili e l'ordinamento di tali valori, ad esempio gli errori vengono sempre visualizzati nella parte superiore della griglia.  
  
-   Errore  
  
-   Scadenza imminente/Scaduta  
  
-   Sottoscrizione non inizializzata  
  
-   Ripetizione comando non riuscito  
  
-   Sincronizzazione in corso  
  
-   Non in sincronizzazione  
  
 L'ordinamento determina inoltre il valore da visualizzare quando per una particolare sottoscrizione sono disponibili più stati. Ad esempio, se per una sottoscrizione sono presenti errori e la scadenza della sottoscrizione è imminente, nella colonna **Stato** viene visualizzato il valore **Errore**.  
  
 I valori di stato **Scadenza imminente/Scaduta** e **Sottoscrizione non inizializzata** sono avvisi. Quando viene visualizzato un avviso, nella colonna **Stato** viene inoltre indicato se è in esecuzione un agente. Ad esempio, lo stato potrebbe essere **In esecuzione, Scadenza imminente/Scaduta**.  
  
 Il valore di stato **Scadenza imminente/Scaduta** viene visualizzato solo se è stato impostato un valore soglia. Per altre informazioni sull'impostazione di valori soglia, vedere [Impostare valori di soglia e avvisi in Monitoraggio replica](monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Sottoscrizione**  
 Il nome di ogni sottoscrizione, nel formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Pubblicazione**  
 Il nome della pubblicazione con cui viene sincronizzata una sottoscrizione, nel formato: *PublicationDatabaseName: PublicationName*.  
  
 **Ultima sincronizzazione**  
 Data e ora dell'ultima esecuzione dell'agente di distribuzione. Se il processo di sincronizzazione è in corso, viene visualizzato **In corso** .  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Monitoraggio della replica](monitoring-replication.md)  
  
  
