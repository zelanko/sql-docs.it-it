---
title: Monitorare e ottimizzare le prestazioni | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fd6fdf81a74e015995f5bf9bd5500f196ccf5cc5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68020255"
---
# <a name="monitor-and-tune-for-performance"></a>Monitoraggio e ottimizzazione delle prestazioni
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  L'obiettivo del monitoraggio dei database consiste nella valutazione delle prestazioni di un server. Un monitoraggio efficace implica l'esecuzione di snapshot periodici delle prestazioni correnti al fine di isolare i processi che causano problemi, nonché la raccolta continua di dati nel tempo per tenere traccia delle tendenze delle prestazioni.  
  
 La valutazione continuativa delle prestazioni del database consente di ridurre al minimo i tempi di risposta e di aumentare al massimo la velocità effettiva, ottimizzando pertanto le prestazioni. Traffico di rete, operazioni di I/O su disco e utilizzo della CPU efficienti sono fattori fondamentali per ottenere prestazioni ottimali. È necessario analizzare accuratamente i requisiti delle applicazioni, comprendere la struttura logica e fisica dei dati, valutare l'utilizzo del database e raggiungere compromessi adeguati tra tipi di utilizzo in conflitto, ad esempio elaborazione delle transazioni online (OLTP) e supporto decisionale.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>Monitoraggio e ottimizzazione del database per le prestazioni  
 In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nel sistema operativo Microsoft Windows sono disponibili utilità che consentono di visualizzare la condizione corrente del database e di tenere traccia delle prestazioni in caso di variazioni. Per il monitoraggio di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile una vasta gamma di strumenti e tecniche. Il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di eseguire queste operazioni:  
  
-   Determinare se è possibile migliorare le prestazioni. Il monitoraggio dei tempi di risposta delle query più frequenti consente, ad esempio, di determinare se sono necessarie modifiche alle query o agli indici nelle tabelle.  
  
-   Valutare le attività degli utenti. Il monitoraggio dei tentativi di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consente ad esempio di determinare se il sistema di sicurezza è adeguatamente impostato e di testare applicazioni e sistemi di sviluppo. Il monitoraggio dell'esecuzione di query SQL consente ad esempio di determinare se le query sono formulate in modo corretto e se producono i risultati previsti.  
  
-   Risolvere problemi o eseguire il debug dei componenti di applicazione, ad esempio di stored procedure.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>Monitoraggio in un ambiente dinamico  
I cambiamenti delle condizioni comportano variazioni nelle prestazioni. Nel corso delle valutazioni, è possibile analizzare le variazioni delle prestazioni in relazione ad aumento del numero di utenti, modifica dei metodi di connessione e accesso degli utenti, aumento dei contenuti del database, cambiamento nelle applicazioni client, variazione dei dati nelle applicazioni, aumento della complessità delle query e incremento del traffico di rete. L'uso di strumenti per il monitoraggio delle prestazioni consente di associare alcune variazioni nelle prestazioni con cambiamenti nelle condizioni e complessità delle query. **Esempi:**  
  
-   Il monitoraggio dei tempi di risposta delle query più frequenti consente di determinare se sono necessarie modifiche alle query o agli indici nelle tabelle in cui le query vengono eseguite.  
  
-   Il monitoraggio dell'esecuzione di query [!INCLUDE[tsql](../../includes/tsql-md.md)] consente di determinare se le query sono formulate in modo corretto e se producono i risultati previsti.  
  
-   Il monitoraggio dei tentativi di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]consente di determinare se il sistema di sicurezza è adeguato e di verificare il funzionamento di applicazioni o sistemi di sviluppo.  
  
I tempi di risposta corrispondono al tempo necessario per la restituzione all'utente della prima riga del set di risultati come conferma visiva dell'elaborazione di una query. La velocità effettiva corrisponde al numero totale di query gestite dal server in un determinato periodo di tempo.  
  
Con l'aumentare del numero di utenti, aumenta la concorrenza per le risorse del server, che a sua volta comporta un incremento dei tempi di risposta e una diminuzione generale della velocità effettiva.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>Attività di monitoraggio e ottimizzazione delle prestazioni  
  
|Argomento| Attività|  
|-----------|----------------------|  
|[Monitorare i componenti di SQL Server](../../relational-databases/performance/monitor-sql-server-components.md)|Procedure necessarie per monitorare qualsiasi componente di SQL Server, ad esempio Monitoraggio attività, eventi estesi, viste e funzioni a gestione dinamica e così via.|  
|[Strumenti per il monitoraggio e l'ottimizzazione delle prestazioni](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|Elenca gli strumenti di monitoraggio e ottimizzazione disponibili con SQL Server, ad esempio Statistiche query dinamiche e Ottimizzazione guidata motore di database.|  
|[Aggiornamento di database mediante l'Assistente ottimizzazione query](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|Mantenere stabili le prestazioni del carico di lavoro durante l'aggiornamento a un livello di compatibilità più recente del database.|  
|[Monitoraggio delle prestazioni tramite Archivio query](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|Usare l'archivio query per acquisire automaticamente una cronologia di query, piani e statistiche di runtime e conservarle per la consultazione.|  
|[Definire una base di riferimento delle prestazioni](../../relational-databases/performance/establish-a-performance-baseline.md)|Come definire una baseline delle prestazioni.|  
|[Isolare i problemi relativi alle prestazioni](../../relational-databases/performance/isolate-performance-problems.md)|Isolare problemi di prestazioni del database.|  
|[Individuare i colli di bottiglia](../../relational-databases/performance/identify-bottlenecks.md)|Monitorare e tenere traccia delle prestazioni del server per identificare colli di bottiglia.|  
|[Usare DMV per determinare le statistiche di utilizzo e le prestazioni delle viste](../../relational-databases/performance/use-dmvs-determine-usage-performance-views.md)|Illustra la metodologia e gli script usati per ottenere informazioni sulle prestazioni delle query.|  
|[Monitoraggio delle prestazioni e dell'attività del server](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|Usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli strumenti di monitoraggio delle prestazioni e delle attività di Windows.|  
|[Monitoraggio dell'utilizzo delle risorse](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|Utilizzo di Monitoraggio di sistema, noto anche come perfmon, per misurare le prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando i contatori delle prestazioni.|  

  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md)    
 [Confrontare e analizzare i piani di esecuzione](../../relational-databases/performance/compare-and-analyze-execution-plans.md)    
 [Visualizzare e salvare piani di esecuzione](../../relational-databases/performance/display-and-save-execution-plans.md)    
  
  
