---
title: Informazioni sulla pubblicazione, Agenti (pubblicazione transazionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e538d324fdd9ce6d17a5583af573711a82b2d946
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133423"
---
# <a name="publication-information-agents-transactional-publication"></a>Informazioni sulla pubblicazione, Agenti (pubblicazione transazionale)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La scheda **Agenti** visualizza informazioni di riepilogo sugli agenti per la pubblicazione selezionata. Le informazioni sull'agente snapshot e sull'agente di lettura log vengono visualizzate per tutte le pubblicazioni transazionali. Le informazioni sull'agente di lettura coda vengono visualizzate per le pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni su un agente e per le attività correlate, fare clic con il pulsante destro del mouse sulla riga dell'agente e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne**.  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne**.  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro**.  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Stato**  
 Stato di ogni agente di replica associato alla pubblicazione. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   In esecuzione  
  
-   Completato  
  
 **Agente**  
 Nome di ogni agente di replica associato alla pubblicazione. L'agente di distribuzione è associato alle sottoscrizioni della pubblicazione. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Durata**  
 Quantità di tempo di esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
  
