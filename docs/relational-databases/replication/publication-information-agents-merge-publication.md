---
description: Informazioni sulla pubblicazione, Agenti (pubblicazione di tipo merge)
title: Informazioni sulla pubblicazione, Agenti (pubblicazione di tipo merge) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.downlevelagents.merge.f1
ms.assetid: 73ff590a-20da-4f10-b592-c60b7226d22b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce84b55a553b26e6fe9141601987f1e743584699
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88493893"
---
# <a name="publication-information-agents-merge-publication"></a>Informazioni sulla pubblicazione, Agenti (pubblicazione di tipo merge)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   La scheda **Agenti** visualizza informazioni di riepilogo sull'agente di snapshot per la pubblicazione selezionata.  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni sull'agente snapshot e sulle attività correlate, fare clic con il pulsante destro del mouse sulla riga dell'agente e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne** .  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne** .  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro** .  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Status**  
 Stato dell'agente snapshot. Nell'elenco seguente vengono indicati i valori di stato possibili:  
  
-   Errore  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   Completato  
  
 **Agent**  
 Agente snapshot. Si tratta dell'unico agente associato a una pubblicazione di tipo merge. L'agente di merge è associato alle sottoscrizioni della pubblicazione. Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 **Ultima ora inizio**  
 Ultima ora di avvio dell'agente.  
  
 **Duration**  
 Quantità di tempo di esecuzione dell'agente. Il valore di durata rappresenta il tempo trascorso se l'agente è ancora in esecuzione e la durata totale se l'agente è stato eseguito in precedenza.  
  
 **Ultima azione**  
 Ultima azione eseguita durante la più recente esecuzione dell'agente.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).
  
  
