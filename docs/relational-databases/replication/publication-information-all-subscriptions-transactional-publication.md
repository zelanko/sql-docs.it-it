---
title: Informazioni sulla pubblicazione, Tutte le sottoscrizioni (Pubblicazione transazionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.allsubscriptions.tran.f1
ms.assetid: 7073350c-f667-4f70-88e9-152c9a1b08dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: efc0ea71d8b2f3b8936e0af7227a2aaccb298674
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120356"
---
# <a name="publication-information-all-subscriptions-transactional-publication"></a>Informazioni sulla pubblicazione, Tutte le sottoscrizioni (Pubblicazione transazionale)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La scheda **Tutte le sottoscrizioni** visualizza informazioni su tutte le sottoscrizioni della pubblicazione transazionale selezionata.  
  
## <a name="options"></a>Opzioni  
 Per ulteriori informazioni su una sottoscrizione e sulle attività correlate, fare clic con il pulsante destro del mouse sulla riga della sottoscrizione e quindi scegliere un'opzione dal menu di scelta rapida. Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne**.  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne**.  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro**.  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Mostra**  
 Solo[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Consente di selezionare gli stati della sottoscrizione da visualizzare per il tipo di sottoscrizione selezionato. Ad esempio, è possibile scegliere di visualizzare solo le sottoscrizioni con errori.  
  
 **Stato**  
 Stato di ogni sottoscrizione determinato dallo stato dell'agente di distribuzione o dell'agente di lettura log. Viene visualizzato lo stato con priorità più alta. Lo stato può inoltre essere determinato dall'agente di lettura coda nel caso in cui vengano utilizzate sottoscrizioni ad aggiornamento in coda.  
  
 Per impostazione predefinita, la griglia contenente le informazioni sulla sottoscrizione viene ordinata in base alla colonna **Stato** e quindi ordinata in base alla colonna **Prestazioni** per le sottoscrizioni che hanno lo stesso stato. Nell'elenco seguente vengono indicati i valori di stato possibili e l'ordinamento di tali valori, ad esempio gli errori vengono sempre visualizzati nella parte superiore della griglia.  
  
-   Errore  
  
-   Prestazioni critiche (solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive).  
  
-   Scadenza imminente/Scaduta (solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive)  
  
-   Sottoscrizione non inizializzata (solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive)  
  
-   Ripetizione comando non riuscito  
  
-   Non in esecuzione  
  
-   In esecuzione  
  
 L'ordinamento determina inoltre il valore da visualizzare quando per una particolare sottoscrizione sono disponibili più stati. Se, ad esempio, per una sottoscrizione sono presenti errori e la scadenza della sottoscrizione è imminente, nella colonna **Stato** sarà visualizzato il valore **Errore**.  
  
 I valori di stato **Prestazioni critiche**, **Scadenza imminente/Scaduta**e **Sottoscrizione non inizializzata** sono avvisi. Quando viene visualizzato un avviso, nella colonna **Stato** viene inoltre visualizzato se è in esecuzione un agente. Ad esempio, lo stato potrebbe essere **In esecuzione, Prestazioni critiche**.  
  
 I valori di stato **Prestazioni critiche** e **Scadenza imminente/Scaduta** vengono visualizzati sono se sono stati impostati valori soglia. Per informazioni sulle misurazioni delle prestazioni e sull'impostazione dei valori soglia, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) e [Impostare valori di soglia e avvisi in Monitoraggio replica](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Sottoscrizione**  
 Nome della sottoscrizione nel formato: *SubscriberName: SubscriptionDatabaseName*.  
  
 **Prestazioni**  
 Solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. La valutazione delle prestazioni per ogni sottoscrizione è basata sulle misure più recenti rilevate da Monitoraggio replica e non riflette le prestazioni cronologiche. Le prestazioni vengono misurate per le sottoscrizioni delle pubblicazioni per le quali sono state definite soglie di prestazione. Se le soglie di prestazione non sono state definite per una pubblicazione, in questa colonna viene visualizzato **Non attivato**. La valutazione delle prestazioni può corrispondere a uno dei valori seguenti:  
  
-   Eccellenti  
  
-   Buone  
  
-   Discrete  
  
-   Scarse  
  
-   Critico  
  
 Se le prestazioni sono critiche, nella colonna **Stato** viene visualizzato **Prestazioni critiche** . Per altre informazioni sulla modalità con cui vengono definite le valutazioni delle prestazioni e impostate le soglie di prestazione, vedere [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Latenza**  
 Solo[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Tempo medio che intercorre tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore. La latenza visualizzata è basata sulle misure più recenti rilevate da Monitoraggio replica. Per altre informazioni sulla misurazione della latenza, vedere [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
