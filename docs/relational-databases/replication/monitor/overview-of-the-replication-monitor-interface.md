---
title: Panoramica dell'interfaccia di Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 078f0e34-7153-45c4-8725-778b5bef88da
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e293625ab72ba1b94b32a1e6c1ada853b88509f4
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770600"
---
# <a name="overview-of-the-replication-monitor-interface"></a>Panoramica dell'interfaccia di Monitoraggio replica
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Monitoraggio replica per[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre una visualizzazione incentrata sul server di pubblicazione o sul server di distribuzione di tutte le attività di replica suddivise in due riquadri. Se si aggiunge un server di pubblicazione nel riquadro sinistro di Monitoraggio replica, verranno visualizzate nel riquadro sinistro informazioni sul server di pubblicazione, sulle relative pubblicazioni, sulle sottoscrizioni a tali pubblicazioni e sui diversi agenti di replica. Oltre a visualizzare informazioni per la topologia di replica, Monitoraggio replica consente di eseguire numerose attività, quali l'avvio e l'arresto degli agenti e la convalida dei dati.  
  
## <a name="viewing-information-for-the-entire-topology"></a>Visualizzazione di informazioni per l'intera topologia  
 Nel riquadro sinistro di Monitoraggio replica vengono visualizzati  
  
-   Gruppi di server di pubblicazione, server di pubblicazione e pubblicazioni.  
  
-   Database di distribuzione, Server di pubblicazione e pubblicazioni.  
  
 Per visualizzare informazioni in Monitoraggio replica, è innanzitutto necessario aggiungere un server di pubblicazione. Per altre informazioni, vedere [Aggiungere e rimuovere server di pubblicazione da Monitoraggio replica](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
 Il riquadro sinistro consente di individuare i seguenti aspetti:  
  
-   Il sistema di replica funziona correttamente?  
  
     Lo stato del sistema di replica è valido se non sono presenti icone di errore sui nodi nel riquadro sinistro. Per ottenere una visione più completa dello stato del sistema, è inoltre consigliabile controllare la scheda **Elenco verifica sottoscrizioni** in cui sono visualizzate informazioni sulle sottoscrizioni che richiedono un'attenzione particolare.  
  
-   Perché l'agente non è in esecuzione?  
  
     Un agente può non essere in esecuzione in un determinato momento perché la sua esecuzione non è pianificata o perché si è verificato un errore. In quest'ultimo caso viene visualizzata un'icona di errore sui nodi appropriati nel riquadro sinistro. Ad esempio, se l'agente snapshot per una pubblicazione è stato arrestato a causa di un errore, viene visualizzata un'icona di errore sul gruppo server di pubblicazione, sul server di pubblicazione e sui nodi di pubblicazione. Le informazioni di riepilogo per l'agente snapshot vengono visualizzate nella scheda **Agenti** per la pubblicazione. Fare doppio clic sull'agente snapshot in questa scheda per visualizzare informazioni dettagliate sull'errore.  
  
## <a name="viewing-information-and-performing-tasks-related-to-distributors"></a>Visualizzazione delle informazioni ed esecuzione di attività relative ai server di distribuzione  
 Monitoraggio replica consente di visualizzare informazioni sui server di distribuzione in tre schede:  
  
-   Scheda**Pubblicazioni**  
  
     In questa scheda sono incluse informazioni di riepilogo per tutte le pubblicazioni di un server di distribuzione.  
  
-   Scheda**Elenco verifica sottoscrizioni**  
  
     In questa scheda sono incluse informazioni sulle sottoscrizioni per il server di distribuzione selezionato. È possibile filtrare l'elenco delle sottoscrizioni per visualizzare errori, avvisi ed eventuali sottoscrizioni con prestazioni scarse. In questa scheda è inoltre possibile effettuare le attività seguenti: accedere alle proprietà di sottoscrizione, accedere a informazioni dettagliate sull'agente o gli agenti associati a una sottoscrizione, reinizializzare le sottoscrizioni e convalidare le sottoscrizioni.  
  
     La scheda **Elenco verifica sottoscrizioni** consente di individuare i seguenti aspetti:  
  
    -   Quali sottoscrizioni sono lente?  
  
         Impostare le opzioni presenti in questa scheda in modo che nella griglia le sottoscrizioni siano disposte in base alle prestazioni offerte.  
  
    -   Il sistema di replica funziona correttamente?  
  
         Nella griglia presente in questa scheda vengono visualizzate icone di errore e di avviso per qualsiasi sottoscrizione che richieda un'attenzione particolare.  
  
     Questa scheda non è disponibile per i server di distribuzione che eseguono versioni di [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o successive.  
  
-   Scheda**Agenti**  
  
     In questa scheda vengono visualizzate informazioni dettagliate su agenti e processi utilizzati da tutti i tipi di replica. La scheda consente anche di avviare e arrestare ciascun agente e processo.  
  
 In Monitoraggio replica è incluso inoltre un menu di scelta rapida per il nodo del server di distribuzione. Fare clic con il pulsante destro del mouse su un server di distribuzione nel riquadro sinistro per effettuare le attività seguenti:  
  
-   Aggiungere un server di pubblicazione a Monitoraggio replica.  
  
-   Modificare le impostazioni di Monitoraggio replica per il server di distribuzione.  
  
-   Passare alla vista Gruppo server di pubblicazione.  
  
## <a name="viewing-information-and-performing-tasks-related-to-publishers"></a>Visualizzazione delle informazioni ed esecuzione di attività relative ai server di pubblicazione  
 Monitoraggio replica consente di visualizzare informazioni sui server di pubblicazione in tre schede:  
  
-   Scheda**Pubblicazioni**  
  
     In questa scheda sono incluse informazioni di riepilogo per tutte le pubblicazioni di un server di pubblicazione.  
  
-   Scheda**Elenco verifica sottoscrizioni**  
  
     Questa scheda è destinata alla visualizzazione delle informazioni sulle sottoscrizioni da tutte le pubblicazioni disponibili nel server di pubblicazione selezionato. È possibile filtrare l'elenco delle sottoscrizioni per visualizzare errori, avvisi ed eventuali sottoscrizioni con prestazioni scarse. In questa scheda è inoltre possibile accedere alle proprietà di sottoscrizione, accedere a informazioni dettagliate sull'agente o gli agenti associati a una sottoscrizione, reinizializzare le sottoscrizioni e convalidare le sottoscrizioni.  
  
     La scheda **Elenco verifica sottoscrizioni** consente di individuare i seguenti aspetti:  
  
    -   Quali sottoscrizioni sono lente?  
  
         Impostare le opzioni presenti in questa scheda in modo che nella griglia le sottoscrizioni siano disposte in base alle prestazioni offerte.  
  
    -   Il sistema di replica funziona correttamente?  
  
         Nella griglia presente in questa scheda vengono visualizzate icone di errore e di avviso per qualsiasi sottoscrizione che richieda un'attenzione particolare.  
  
     Questa scheda non viene visualizzata per i server di distribuzione che eseguono versioni precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   Scheda**Agenti**  
  
     In questa scheda vengono visualizzate informazioni dettagliate su agenti e processi utilizzati da tutti i tipi di replica. La scheda consente anche di avviare e arrestare ciascun agente e processo.  
  
 Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività relative a un server di pubblicazione &#40;Monitoraggio replica&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 In Monitoraggio replica è incluso inoltre un menu di scelta rapida per il nodo del server di pubblicazione. Fare clic con il pulsante destro del mouse su un server di pubblicazione nel riquadro sinistro per:  
  
-   Modificare le impostazioni di Monitoraggio replica per il server di pubblicazione  
  
-   Rimuovere il server di pubblicazione da Monitoraggio replica  
  
-   Visualizzare e modificare i profili dell'agente  
  
-   Connettersi o disconnettersi dal server di distribuzione in cui sono archiviate informazioni sul server di pubblicazione  
  
## <a name="viewing-information-and-performing-tasks-related-to-publications"></a>Visualizzazione delle informazioni ed esecuzione di attività relative alle pubblicazioni  
 In Monitoraggio replica vengono visualizzate informazioni sulle pubblicazioni in tre schede e in alcune finestre dei dettagli:  
  
-   Scheda**Tutte le sottoscrizioni**  
  
     In questa scheda vengono visualizzate informazioni su tutte le sottoscrizioni della pubblicazione selezionata. Per impostazione predefinita, le informazioni disponibili in questa scheda vengono visualizzate in ordine di priorità: errori, avvisi e sottoscrizioni ordinate in base alle prestazioni, dalle più scarse alle migliori.  
  
     La scheda **Tutte le sottoscrizioni** consente di individuare i seguenti aspetti:  
  
    -   Quali sottoscrizioni sono lente?  
  
         Impostare le opzioni presenti in questa scheda in modo che nella griglia le sottoscrizioni siano disposte in base alle prestazioni offerte.  
  
    -   Il sistema di replica funziona correttamente?  
  
         Nella griglia presente in questa scheda vengono visualizzate icone di errore e di avviso per qualsiasi sottoscrizione che richieda un'attenzione particolare.  
  
-   Scheda**Agenti**  
  
     In questa scheda vengono visualizzate informazioni sugli agenti utilizzati dalla replica. In questa scheda vengono visualizzate informazioni relative agli agenti seguenti:  
  
    -   Agente snapshot, utilizzato da tutte le pubblicazioni.  
  
    -   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.  
  
    -   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
     Questa scheda consente inoltre di accedere a informazioni dettagliate su ciascun agente, nonché di avviare e arrestare ciascun agente. Per informazioni sugli agenti associati alle sottoscrizioni (agente di distribuzione e agente di merge), vedere la sezione "Visualizzazione delle informazioni ed esecuzione di attività relative alle sottoscrizioni" in questo argomento.  
  
-   Scheda**Avvisi**  
  
     Questa scheda consente di specificare avvisi per gli agenti. Per altre informazioni, vedere [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Scheda**Token di traccia** (solo nella replica transazionale)  
  
     Questa scheda consente di misurare la latenza, ovvero l'intervallo di tempo che intercorre tra il commit di una transazione nel server di pubblicazione e il commit della transazione corrispondente nel Sottoscrittore.  
  
     Questa scheda consente di individuare i seguenti aspetti:  
  
    -   In quanto tempo una transazione di cui è stato appena eseguito il commit raggiungerà un Sottoscrittore nella replica transazionale?  
  
         È possibile visualizzare l'intervallo di tempo impiegato da una transazione per attraversare il sistema e paragonare questo valore con gli intervalli precedenti.  
  
     Questa scheda non viene visualizzata per i server di distribuzione che eseguono [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o versioni precedenti. Per altre informazioni sui token di traccia, vedere [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
-   Finestre dei dettagli per gli agenti associati a una pubblicazione. Alle pubblicazioni sono associati i seguenti agenti:  
  
    -   Agente snapshot, utilizzato da tutte le pubblicazioni.  
  
    -   Agente di lettura log, utilizzato da tutte le pubblicazioni transazionali.  
  
    -   Agente di lettura coda, utilizzato dalle pubblicazioni transazionali abilitate per le sottoscrizioni ad aggiornamento in coda.  
  
     Fare doppio clic su un agente in Monitoraggio replica per accedere alle informazioni in una finestra dei dettagli. Oltre agli agenti elencati sopra, sono disponibili agenti associati alle sottoscrizioni: l'agente di distribuzione per sottoscrizioni a pubblicazioni snapshot e transazionali e l'agente di merge per sottoscrizioni a pubblicazioni di tipo merge. Per ulteriori informazioni, vedere la sezione "Visualizzazione delle informazioni ed esecuzione di attività relative alle sottoscrizioni" in questo argomento.  
  
     Le finestre dei dettagli sugli agenti includono informazioni sulle sessioni dell'agente, specificando l'ora di inizio, l'ora di fine, la durata e le azioni eseguite in una sessione. Queste finestre consentono di individuare i seguenti aspetti:  
  
    -   Perché l'agente non è in esecuzione?  
  
         I messaggi di errore disponibili offrono informazioni dettagliate sul motivo per cui un agente non è in esecuzione e rappresentano un punto di partenza per la risoluzione di problemi relativi agli agenti associati a una pubblicazione.  
  
 Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Monitoraggio replica include inoltre un menu di scelta rapida per il nodo delle pubblicazioni. Fare clic con il pulsante destro del mouse su una pubblicazione nel riquadro sinistro per:  
  
-   Reinizializzare tutte le sottoscrizioni di una pubblicazione  
  
-   Convalidare tutte le sottoscrizioni di una pubblicazione  
  
-   Generare uno snapshot per una pubblicazione  
  
-   Visualizzare e modificare le proprietà della pubblicazione  
  
## <a name="viewing-information-and-performing-tasks-related-to-subscriptions"></a>Visualizzazione delle informazioni ed esecuzione di attività relative alle sottoscrizioni  
 In Monitoraggio replica vengono visualizzate informazioni sulle sottoscrizioni all'interno di numerose schede. Fare doppio clic su una sottoscrizione in Monitoraggio replica per accedere a tali schede in una finestra dei dettagli. Tutte le schede consentono di individuare i motivi per cui un agente non è in esecuzione. I messaggi di errore disponibili offrono informazioni dettagliate sul motivo per cui un agente non è in esecuzione e rappresentano un punto di partenza per la risoluzione di problemi relativi agli agenti associati a una sottoscrizione.  
  
-   Schede**Tutte le sottoscrizioni** e **Elenco verifica sottoscrizioni**.  
  
     Queste schede sono descritte più indietro in questo argomento.  
  
-   Scheda**Cronologia server di pubblicazione - server di distribuzione** (solo nella replica transazionale)  
  
     In questa scheda vengono visualizzate informazioni sull'agente di lettura log per una pubblicazione (la scheda è identica alla finestra dei dettagli Agente di lettura log).  
  
-   Scheda**Cronologia server di distribuzione - Sottoscrittore** (nella replica snapshot e nella replica transazionale)  
  
     In questa scheda vengono visualizzate informazioni sull'agente di distribuzione per una sottoscrizione.  
  
-   Scheda**Comandi non distribuiti** (solo nella replica transazionale)  
  
     In questa scheda vengono visualizzate informazioni sul numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato e sul tempo stimato per recapitare tali comandi. Questa scheda consente di individuare lo stato della sottoscrizione è non è disponibile per i server di distribuzione che eseguono versioni precedenti a SQL Server 2005.  
  
-   Scheda**Cronologia sincronizzazione** (solo nella replica di tipo merge)  
  
     In questa scheda vengono visualizzate informazioni sull'agente di merge per una sottoscrizione. Questa scheda consente di individuare i seguenti aspetti:  
  
    -   Per quale motivo la sottoscrizione di tipo merge è lenta?  
  
         In questa scheda vengono incluse statistiche dettagliate per ogni articolo elaborato durante la sincronizzazione, incluso l'intervallo di tempo impiegato in ogni fase di elaborazione (caricamento delle modifiche, download delle modifiche e così via). Questa scheda può agevolare l'identificazione di tabelle specifiche che causano rallentamenti ed è il luogo ideale per risolvere problemi relativi alle prestazioni delle sottoscrizioni di tipo merge.  
  
 Per altre informazioni, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).
  
## <a name="viewing-information-and-performing-tasks-related-to-agent-profiles"></a>Visualizzazione delle informazioni ed esecuzione di attività relative ai profili degli agenti  
 Monitoraggio replica include un certo numero di finestre di dialogo per la gestione dei profili degli agenti. I profili degli agenti sono set di parametri relativi a un agente che ne determinano il comportamento. Per altre informazioni, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md). Di seguito vengono descritte le finestre di dialogo associate ai profili:  
  
-   **Profili agenti**  
  
     In questa finestra di dialogo è possibile modificare le proprietà dei profili, creare ed eliminare i profili, specificare un profilo predefinito e specificare che tutti gli agenti di un tipo specifico, ad esempio gli agenti snapshot, debbano utilizzare un determinato profilo.  
  
-   **\<NomeProfiloAgente> Proprietà**  
  
     Questa finestra di dialogo consente di visualizzare e modificare le impostazioni dei parametri in un profilo.  
  
-   **Nuovo profilo agente**  
  
     Questa finestra di dialogo consente di creare un nuovo profilo, che può facoltativamente includere i valori di un profilo esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
