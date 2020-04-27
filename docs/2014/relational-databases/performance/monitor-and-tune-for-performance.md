---
title: Monitorare e ottimizzare le prestazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 683e8044b235828741fe429f133af82d1977031a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150712"
---
# <a name="monitor-and-tune-for-performance"></a>Monitoraggio e ottimizzazione delle prestazioni
  L'obiettivo del monitoraggio dei database consiste nella valutazione delle prestazioni di un server. Un monitoraggio efficace implica l'esecuzione di snapshot periodici delle prestazioni correnti al fine di isolare i processi che causano problemi, nonché la raccolta continua di dati nel tempo per tenere traccia delle tendenze delle prestazioni.  
  
 La valutazione continuativa delle prestazioni del database consente di ridurre al minimo i tempi di risposta e di aumentare al massimo la velocità effettiva, ottimizzando pertanto le prestazioni. Traffico di rete, operazioni di I/O su disco e utilizzo della CPU efficienti sono fattori fondamentali per ottenere prestazioni ottimali. È necessario analizzare accuratamente i requisiti delle applicazioni, comprendere la struttura logica e fisica dei dati, valutare l'utilizzo del database e raggiungere compromessi adeguati tra tipi di utilizzo in conflitto, ad esempio elaborazione delle transazioni online (OLTP) e supporto decisionale.  
  
## <a name="benefits-of-monitoring-and-tuning-databases-for-performance"></a>Vantaggi del monitoraggio e dell'ottimizzazione del database per le prestazioni  
 In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nel sistema operativo Microsoft Windows sono disponibili utilità che consentono di visualizzare la condizione corrente del database e di tenere traccia delle prestazioni in caso di variazioni. Sono disponibili diversi strumenti e tecniche che è possibile utilizzare per monitorare [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di:  
  
-   Determinare se è possibile migliorare le prestazioni. Il monitoraggio dei tempi di risposta delle query più frequenti consente, ad esempio, di determinare se sono necessarie modifiche alle query o agli indici nelle tabelle.  
  
-   Valutare le attività degli utenti. Il monitoraggio dei tentativi di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consente ad esempio di determinare se il sistema di sicurezza è adeguatamente impostato e di testare applicazioni e sistemi di sviluppo. Il monitoraggio dell'esecuzione di query SQL consente ad esempio di determinare se le query sono formulate in modo corretto e se producono i risultati previsti.  
  
-   Risolvere eventuali problemi o eseguire il debug dei componenti di applicazione, ad esempio di stored procedure.  
  
### <a name="monitoring-in-a-dynamic-environment"></a>Monitoraggio in un ambiente dinamico  
 Il monitoraggio è importante perché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un servizio in un ambiente dinamico. I cambiamenti delle condizioni comportano variazioni nelle prestazioni. Nel corso delle valutazioni, è possibile analizzare le variazioni delle prestazioni in relazione ad aumento del numero di utenti, modifica dei metodi di connessione e accesso degli utenti, aumento dei contenuti del database, cambiamento nelle applicazioni client, variazione dei dati nelle applicazioni, aumento della complessità delle query e incremento del traffico di rete. Utilizzando gli strumenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il monitoraggio delle prestazioni, è possibile associare alcune variazioni nelle prestazioni con cambiamenti nelle condizioni e complessità delle query. Gli scenari illustrati di seguito offrono alcuni esempi:  
  
-   Il monitoraggio dei tempi di risposta delle query più frequenti consente di determinare se sono necessarie modifiche alle query o agli indici nelle tabelle in cui le query vengono eseguite.  
  
-   Il monitoraggio dell'esecuzione di query [!INCLUDE[tsql](../../includes/tsql-md.md)] consente di determinare se le query sono formulate in modo corretto e se producono i risultati previsti.  
  
-   Il monitoraggio dei tentativi di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consente di determinare se il sistema di sicurezza è adeguato e di verificare il funzionamento di applicazioni o sistemi di sviluppo.  
  
 I tempi di risposta corrispondono al tempo necessario per la restituzione all'utente della prima riga del set di risultati come conferma visiva dell'elaborazione di una query. La velocità effettiva corrisponde al numero totale di query gestite dal server in un determinato periodo di tempo.  
  
 Con l'aumentare del numero di utenti, aumenta la concorrenza per le risorse del server, che a sua volta comporta un incremento dei tempi di risposta e una diminuzione generale della velocità effettiva.  
  
## <a name="monitoring-and-tuning-performance-tasks"></a>Attività di monitoraggio e ottimizzazione delle prestazioni  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|[Monitorare i componenti di SQL Server](monitor-sql-server-components.md)|Fornisce i passaggi necessari richiesti per esaminare efficacemente qualsiasi componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](performance-monitoring-and-tuning-tools.md)|Vengono elencati gli strumenti di monitoraggio e ottimizzazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Definire una base di riferimento delle prestazioni](establish-a-performance-baseline.md)|Fornisce informazioni su come stabilire un riferimento per le prestazioni.|  
|[Isolare i problemi relativi alle prestazioni](isolate-performance-problems.md)|Viene descritto come isolare problemi di prestazioni del database.|  
|[Individuare i colli di bottiglia](identify-bottlenecks.md)|Viene descritto come monitorare e tenere traccia delle prestazioni del server per identificare colli di bottiglia.|  
|[Monitoraggio delle prestazioni e dell'attività del server](server-performance-and-activity-monitoring.md)|Viene descritto come utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli strumenti di monitoraggio delle prestazioni e dell'attività di Windows.|  
|[Visualizzare e salvare piani di esecuzione](display-and-save-execution-plans.md)|Viene descritto come visualizzare e salvare piani di esecuzione in un file in formato XML.|  
|[Monitoraggio delle prestazioni con Archivio query](monitoring-performance-by-using-the-query-store.md)|L'archivio di query acquisisce automaticamente una cronologia delle query, dei piani e delle statistiche di runtime e li conserva per la consultazione.|  
  
## <a name="see-also"></a>Vedi anche  
 [Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md)   
 [Monitorare l'utilizzo delle risorse &#40;monitoraggio di sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
