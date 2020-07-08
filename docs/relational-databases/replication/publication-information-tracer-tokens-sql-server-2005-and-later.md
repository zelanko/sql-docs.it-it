---
title: Token di traccia (informazioni sulla pubblicazione)
description: Descrizione della scheda "Token di traccia" della pagina delle informazioni sulla pubblicazione disponibile in Monitoraggio replica all'interno di SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 60d826f519af20e51bc23e8a503975e8222da1bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720949"
---
# <a name="publication-information-tracer-tokens-sql-server-2005-and-later"></a>Informazioni sulla pubblicazione, Token di traccia (SQL Server 2005 e versioni successive)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La scheda **Token di traccia** consente di convalidare le connessioni e di misurare la latenza di un sistema che utilizza la replica transazionale. Un token, ovvero una piccola quantità di dati, viene scritto nel log delle transazioni del database di pubblicazione, contrassegnato come se fosse una comune transazione replicata e inviato tramite il sistema in modo da consentire:  
  
-   Il calcolo del tempo che trascorre tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'inserimento del comando corrispondente nel database di distribuzione del server di distribuzione.  
  
-   Il calcolo del tempo che trascorre tra l'inserimento di un comando nel database di distribuzione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore.  
  
 I risultati ottenuti da questi calcoli consentono all'utente di rispondere a una serie di domande, incluse le seguenti:  
  
-   Quali Sottoscrittori hanno richiesto più tempo per ricevere una modifica dal server di pubblicazione?  
  
-   Tra i Sottoscrittori destinati a ricevere il token di traccia, quali non lo hanno eventualmente ricevuto?  
  
## <a name="options"></a>Opzioni  
 Per modificare la modalità di visualizzazione dei dati nella griglia, fare clic con il pulsante destro del mouse sulla griglia, quindi scegliere una delle opzioni seguenti:  
  
-   **Ordinamento**: consente di ordinare una o più colonne nella finestra di dialogo **Ordina colonne** .  
  
-   **Seleziona colonne da visualizzare**: consente di selezionare le colonne da visualizzare e l'ordine di visualizzazione nella finestra di dialogo **Seleziona colonne** .  
  
-   **Filtro**: consente di filtrare le righe nella griglia in base a valori di colonna nella finestra di dialogo **Impostazioni filtro** .  
  
-   **Cancella filtro**: consente di cancellare qualsiasi impostazione di filtro per la griglia.  
  
 Le impostazioni di filtro sono specifiche di ogni griglia. La selezione e l'ordinamento delle colonne vengono applicati a tutte le griglie dello stesso tipo, ad esempio la griglia delle pubblicazioni per ogni server di pubblicazione.  
  
 **Inserisci utilità di traccia**  
 Fare clic su questo pulsante per inserire un token di traccia nel log delle transazioni del server di pubblicazione.  
  
 **Ora di inserimento**  
 Selezionare l'ora in cui è stato inserito un token di traccia per visualizzare le informazioni sulla latenza a partire da tale ora. Per impostazione predefinita, vengono visualizzate le informazioni a partire dall'ora più recente.  
  
> [!NOTE]  
>  Le informazioni sul token di traccia vengono mantenute per lo stesso periodo di tempo degli altri dati cronologici, ovvero in base all'impostazione del periodo di memorizzazione della cronologia del database di distribuzione. Per informazioni sulla modifica delle proprietà del database di distribuzione, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
 **Sottoscrizione**  
 Nome di ogni sottoscrizione della pubblicazione.  
  
 **Dal server di pubblicazione al server di distribuzione**  
 Tempo trascorso tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'inserimento del comando corrispondente nel database di distribuzione del server di distribuzione. Il valore **In sospeso** indica che il token non ha ancora raggiunto il server di distribuzione. Se lo stato In sospeso persiste, assicurarsi che l'agente di lettura log sia in esecuzione.  
  
 **Dal server di distribuzione al Sottoscrittore**  
 Tempo trascorso tra l'inserimento di un comando nel database di distribuzione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore. Il valore **In sospeso** indica che il token non ha ancora raggiunto il Sottoscrittore. Se lo stato In sospeso persiste, assicurarsi che l'agente di distribuzione sia in esecuzione.  
  
 **Latenza totale**  
 Tempo trascorso tra l'esecuzione del commit di una transazione nel server di pubblicazione e l'esecuzione del commit della transazione corrispondente nel Sottoscrittore. Rappresenta la latenza end-to-end del sistema di replica per il Sottoscrittore corrente nel momento specifico. Il valore **In sospeso** indica che il token non ha ancora raggiunto il Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Misurare la latenza e convalidare le connessioni per la replica transazionale](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
