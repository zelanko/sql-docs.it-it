---
title: Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 60586083e8bdfe7f0227db605d9f36d50a59ef0d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049356"
---
# <a name="view-information-and-perform-tasks-using-replication-monitor"></a>Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica
Monitoraggio replica offre schede e opzioni per visualizzare le informazioni ed eseguire diverse attività. Questo articolo descrive le informazioni che possono essere visualizzate e le operazioni che possono essere eseguite usando Monitoraggio replica.

## <a name="for-a-publication"></a>Per una pubblicazione

### <a name="view-information"></a>Visualizzare informazioni

  In Monitoraggio replica sono disponibili le schede seguenti che includono le informazioni sulla pubblicazione selezionata:  
  
-   **Tutte le sottoscrizioni** : questa scheda Visualizza le informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Agents** -in questa scheda vengono visualizzate informazioni su tutti gli agenti utilizzati da una pubblicazione:  
  
    -   Agente snapshot, utilizzato da tutte le pubblicazioni.    
    -   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.    
    -   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali contenenti sottoscrizioni ad aggiornamento in coda.  
  
-   **Avvisi** (per server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive)   
    -   Questa scheda consente di specificare avvisi per gli agenti.  
  
-   **Token di traccia** (solo replica transazionale, per server di distribuzione che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versioni successive).  
  
     Questa scheda consente di misurare la latenza, ovvero l'intervallo di tempo che intercorre tra il commit di una transazione nel server di pubblicazione e il commit della transazione corrispondente nel Sottoscrittore.  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="perform-tasks"></a>Eseguire attività
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.    
2.  Per visualizzare e modificare le proprietà della pubblicazione, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Proprietà**.    
3.  Per visualizzare le informazioni sulle sottoscrizioni, fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
     Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività in questa scheda. Per ulteriori informazioni, vedere [visualizzare le informazioni ed eseguire attività tramite Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).  
  
4.  Per visualizzare le informazioni sugli agenti, fare clic sulla scheda **agenti** . È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività in questa scheda. Per ulteriori informazioni, vedere [visualizzare le informazioni ed eseguire attività tramite Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).    
5.  Per visualizzare le informazioni sugli avvisi e le soglie degli agenti, fare clic sulla scheda **avvisi** . Per ulteriori informazioni, vedere [impostare soglie e avvisi in Monitoraggio replica](set-thresholds-and-warnings-in-replication-monitor.md).   
6.  Per visualizzare le informazioni sui token di traccia, fare clic sulla scheda **token di traccia** . Per ulteriori informazioni sull'utilizzo dei token di traccia, vedere [misurare la latenza e convalidare le connessioni per la replica transazionale](measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="for-a-publisher"></a>Per un server di pubblicazione
  In Monitoraggio replica sono disponibili le schede seguenti in cui vengono visualizzate informazioni sul server di pubblicazione selezionato:  
  
-   **Pubblicazioni** : questa scheda Visualizza le informazioni su tutte le pubblicazioni nel server di pubblicazione selezionato.  
  
-   **Elenco** verifica sottoscrizioni: questa scheda consente di visualizzare informazioni sulle sottoscrizioni di tutte le pubblicazioni disponibili nel server di pubblicazione selezionato che presentano errori, avvisi o prestazioni più ridotte. Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni precedenti a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Scheda **agenti** : questa scheda consente di visualizzare informazioni dettagliate sugli agenti e sui processi utilizzati da tutti i tipi di replica. La scheda consente anche di avviare e arrestare ciascun agente e processo.  
  
 Per visualizzare ulteriori informazioni sulle opzioni disponibili nelle singole schede, fare clic sulla scheda nel riquadro destro e quindi su **?** nella barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Visualizzare informazioni ed eseguire attività
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro e quindi fare clic su un server di pubblicazione.    
2.  Per visualizzare informazioni su tutte le pubblicazioni, fare clic sulla scheda **Pubblicazioni** .    
3.  Per visualizzare le informazioni sulle sottoscrizioni, fare clic sulla scheda **elenco** verifica sottoscrizioni. È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività da questa scheda:    
    -   Per visualizzare informazioni dettagliate sull'agente associato a una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**.    
    -   Per visualizzare le proprietà di una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**.    
    -   Per sincronizzare una sottoscrizione push, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.    
    -   Per reinizializzare una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Reinizializza sottoscrizione**.   
4.  Per visualizzare le informazioni sugli agenti, fare clic sulla scheda **agenti** . È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività in questa scheda:    
    -   Per visualizzare informazioni dettagliate su un agente, ad esempio messaggi informativi ed eventuali messaggi di errore, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Visualizza dettagli**.    
    -   Per visualizzare informazioni dettagliate sul processo eseguito dall'agente, ad esempio la pianificazione, i dettagli sui passaggi del processo e così via, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Proprietà**.    
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).    
    -   Per avviare un agente non in esecuzione, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Avvia agente**.    
    -   Per arrestare l'esecuzione di un agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Arresta agente**.  
  
## <a name="for-a-subscription"></a>Per una sottoscrizione 

  In Monitoraggio replica sono disponibili le schede seguenti, che includono informazioni sulle sottoscrizioni:  
  
-   **Tutte le sottoscrizioni** : questa scheda Visualizza le informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Elenco** verifica sottoscrizioni: questa scheda consente di visualizzare informazioni sulle sottoscrizioni di tutte le pubblicazioni disponibili nel server di pubblicazione selezionato che presentano errori, avvisi o prestazioni più ridotte. Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="all-subscriptions-tab"></a>Scheda tutte le sottoscrizioni  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.   
2.  Per visualizzare le informazioni sulle sottoscrizioni, fare clic sulla scheda **Tutte le sottoscrizioni** . Per visualizzare solo le sottoscrizioni in uno stato specifico, ad esempio in sincronizzazione, selezionare un'opzione nell'elenco a discesa **Mostra** .   
3.  Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività in questa scheda. Per ulteriori informazioni, vedere [visualizzare le informazioni ed eseguire attività tramite Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).  
  
### <a name="subscription-watch-list-tab"></a>Scheda Elenco verifica sottoscrizioni  
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro e quindi fare clic su un server di pubblicazione.   
2.  Per visualizzare informazioni sulle sottoscrizioni, fare clic sulla scheda **Elenco verifica sottoscrizioni** .  
3.  Selezionare il tipo di sottoscrizione da visualizzare nell'elenco a discesa **Mostra \<SubscriptionType> sottoscrizioni** . Per visualizzare solo le sottoscrizioni in uno stato specifico, ad esempio in sincronizzazione, selezionare un'opzione nell'elenco a discesa **Mostra** .    
4.  Per visualizzare e modificare le proprietà della sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Proprietà**. È inoltre possibile accedere a informazioni più dettagliate ed eseguire attività in questa scheda. Per ulteriori informazioni, vedere [visualizzare le informazioni ed eseguire attività tramite Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).  

## <a name="for-publication-agents"></a>Per gli agenti di pubblicazione

  In Monitoraggio replica è disponibile la scheda **Agenti** , in cui sono presenti informazioni sugli agenti associati alla pubblicazione selezionata. Le agente di distribuzione e agente di merge sono associate alle sottoscrizioni. Per ulteriori informazioni, vedere [visualizzare le informazioni ed eseguire attività tramite Monitoraggio replica](view-information-and-perform-tasks-replication-monitor.md).  
  
 In questa scheda vengono visualizzate informazioni relative agli agenti seguenti:    
-   Agente snapshot, utilizzato da tutte le pubblicazioni.    
-   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.    
-   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
 Per visualizzare altre informazioni relative alle opzioni della scheda, fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Visualizzare informazioni ed eseguire attività 
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.    
2.  Per visualizzare le informazioni sugli agenti, fare clic sulla scheda **Agenti** . In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:  
  
    -   Per visualizzare informazioni dettagliate su un agente, ad esempio messaggi informativi ed eventuali messaggi di errore, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Visualizza dettagli**.    
    -   Per visualizzare informazioni dettagliate sul processo eseguito dall'agente, ad esempio la pianificazione, i dettagli sui passaggi del processo e così via, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Proprietà**.    
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
    -   Per avviare un agente non in esecuzione, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Avvia agente**.  
      -   Per arrestare l'esecuzione di un agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Arresta agente**.  

## <a name="for-subscription-agents"></a>Per gli agenti di sottoscrizione

### <a name="view-information-and-perform-tasks"></a>Visualizzare le informazioni ed eseguire attività
  In Monitoraggio replica sono disponibili due schede che consentono di accedere a informazioni sugli agenti associati a una sottoscrizione:  
  
-   **Tutte le sottoscrizioni** : questa scheda Visualizza le informazioni su tutte le sottoscrizioni della pubblicazione selezionata.  
  
-   **Elenco** verifica sottoscrizioni: questa scheda consente di visualizzare informazioni sulle sottoscrizioni di tutte le pubblicazioni disponibili nel server di pubblicazione selezionato che presentano errori, avvisi o prestazioni più ridotte. Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Per ulteriori informazioni sulle opzioni di ogni scheda, fare clic sulla scheda nel riquadro a destra e quindi fare clic su **?** sulla barra dei menu. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="view-information-and-perform-tasks"></a>Visualizzare informazioni ed eseguire attività 
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.   
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** per visualizzare le informazioni relative alle sottoscrizioni. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:  
  
    -   Per visualizzare informazioni dettagliate sull'agente associato a una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**. Le informazioni dettagliate includono la cronologia dell'agente e i messaggi di errore, statistiche sulle prestazioni nella replica transazionale e statistiche sulla sincronizzazione dei singoli articoli nella replica di tipo merge.    
         A seconda del tipo di sottoscrizione dalla finestra dei dettagli vengono avviate schede diverse: per le sottoscrizioni snapshot la scheda **Cronologia server di distribuzione - Sottoscrittore**, per le sottoscrizioni transazionali le schede **Cronologia server di pubblicazione - server di distribuzione**, **Cronologia server di distribuzione - Sottoscrittore**e **Comandi non distribuiti**e per le sottoscrizioni di tipo merge la scheda **Cronologia sincronizzazione**.    
    -   Per sincronizzare una sottoscrizione push, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.    
    -   Per reinizializzare una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Reinizializza sottoscrizione**.    
    -   Per convalidare una singola sottoscrizione di tipo merge, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Convalida sottoscrizione**. Per convalidare tutte le sottoscrizioni di una pubblicazione di tipo merge, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida tutte le sottoscrizioni**. Per convalidare tutte le sottoscrizioni di una pubblicazione transazionale, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida sottoscrizioni**.    
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
  
### <a name="view-information-and-perform-tasks"></a>Visualizzare informazioni ed eseguire attività
  
1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro e quindi fare clic su un server di pubblicazione.   
2.  Fare clic sulla scheda **Elenco verifica sottoscrizioni** per visualizzare le informazioni relative alle sottoscrizioni. In questa scheda è inoltre possibile accedere a informazioni più dettagliate ed eseguire altre attività:    
    -   Per visualizzare informazioni dettagliate sull'agente associato a una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**. Le informazioni dettagliate includono la cronologia dell'agente e i messaggi di errore, statistiche sulle prestazioni nella replica transazionale e statistiche sulla sincronizzazione dei singoli articoli nella replica di tipo merge.    
         A seconda del tipo di sottoscrizione dalla finestra dei dettagli vengono avviate schede diverse: per le sottoscrizioni snapshot la scheda **Cronologia server di distribuzione - Sottoscrittore**, per le sottoscrizioni transazionali le schede **Cronologia server di pubblicazione - server di distribuzione**, **Cronologia server di distribuzione - Sottoscrittore**e **Prestazioni**e per le sottoscrizioni di tipo merge la scheda **Cronologia sincronizzazione**.    
    -   Per sincronizzare una sottoscrizione push, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.    
    -   Per reinizializzare una sottoscrizione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Reinizializza sottoscrizione**.    
    -   Per convalidare una singola sottoscrizione di tipo merge, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Convalida sottoscrizione**. Per convalidare tutte le sottoscrizioni di una pubblicazione di tipo merge, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida tutte le sottoscrizioni**. Per convalidare tutte le sottoscrizioni di una pubblicazione transazionale, fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Convalida sottoscrizioni**.    
    -   Per gestire i profili dell'agente, fare clic con il pulsante destro del mouse sull'agente e quindi scegliere **Profilo agente**. Per altre informazioni, vedere [Usare i profili agenti di replica](../agents/replication-agent-profiles.md).  
  

## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../publish/view-and-modify-publication-properties.md)   
 [Monitoraggio della replica](../monitoring-replication.md)  
  