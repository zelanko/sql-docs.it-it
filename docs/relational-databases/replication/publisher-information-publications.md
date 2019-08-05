---
title: Informazioni del server di pubblicazione - Pubblicazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: a0590a339b6357bdc102420c4c68d4a92fc0519c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68764077"
---
# <a name="publisher-information-publications"></a>Informazioni del server di pubblicazione - Pubblicazioni
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Nella scheda **Pubblicazioni** vengono fornite informazioni di riepilogo relative a tutte le pubblicazioni nel server di pubblicazione selezionato nel riquadro sinistro.  
  
## <a name="options"></a>Opzioni  
 Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne**.  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne**.  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro**.  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Stato**  
 Stato di ogni pubblicazione determinato in base allo stato di priorità più elevata delle rispettive sottoscrizioni. Per impostazione predefinita, la griglia contenente le informazioni relative alle pubblicazioni viene ordinata in base alla colonna **Stato** . Nell'elenco seguente vengono indicati i valori di stato possibili e l'ordinamento di tali valori, ad esempio gli errori vengono sempre visualizzati nella parte superiore della griglia.  
  
-   Errore  
  
-   Prestazioni critiche  
  
-   Ripetizione comando non riuscito  
  
-   OK  
  
 Il valore di stato **Prestazioni critiche** fa riferimento alle sottoscrizioni di tipo merge e a quelle transazionali. Per queste ultime, il valore può essere visualizzato solo se è impostata una soglia. Per informazioni sulle misurazioni delle prestazioni e sull'impostazione dei valori soglia, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) e [Impostare valori di soglia e avvisi in Monitoraggio replica](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Pubblicazione**  
 Nome di ogni pubblicazione nel formato: *PublicationDatabaseName: PublicationName*.  
  
 **Sottoscrizioni**  
 Numero di sottoscrizioni per ogni pubblicazione.  
  
 **Sincronizzazione in corso**  
 Numero di sottoscrizioni per ogni pubblicazione delle quali è in corso la sincronizzazione:  
  
-   Per la replica transazionale, lo stato di sincronizzazione in corso indica che l'agente di distribuzione è in esecuzione ma non necessariamente che i dati vengono replicati.  
  
-   Per la replica di tipo merge, lo stato di sincronizzazione in corso indica che l'agente di merge è in esecuzione e che i dati vengono replicati.  
  
-   Per la replica snapshot, lo stato di sincronizzazione in corso indica che l'agente di distribuzione è in esecuzione e che i dati vengono replicati.  
  
 **Prestazioni medie correnti** e **Prestazioni peggiori correnti**  
 Solo[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Valutazione delle prestazioni medie e di quelle peggiori rispettivamente indicate per tutte le sottoscrizioni di una pubblicazione. Le valutazioni si basano sulle misurazioni più recenti eseguite dallo strumento Monitoraggio replica e non riflettono il livello di prestazioni di una sottoscrizione nel tempo.  
  
 Per la replica transazionale, in Monitoraggio replica viene visualizzato un valore solo per le pubblicazioni per le quali sono definite soglie di prestazioni. Se non sono impostati valori per le soglie delle prestazioni, in questa colonna viene visualizzato il valore **Non attivato**. Per la replica di tipo merge, in Monitoraggio replica viene visualizzato un valore dopo cinque sincronizzazioni con 50 o più modifiche eseguite con lo stesso tipo di connessione (remota o LAN). Se sono state eseguite meno di 5 sincronizzazioni con almeno 50 modifiche oppure durante la sincronizzazione più recente sono state apportate meno di 50 modifiche, la colonna è vuota.  
  
 La valutazione delle prestazioni può corrispondere a uno dei valori seguenti:  
  
-   Eccellenti  
  
-   Buone  
  
-   Discrete  
  
-   Scarse  
  
-   Critico  
  
 Per altre informazioni sulla modalità con cui vengono definite le valutazioni delle prestazioni e impostati i valori soglia per le prestazione, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
