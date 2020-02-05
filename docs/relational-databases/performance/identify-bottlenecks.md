---
title: Individuare i colli di bottiglia | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource bottlenecks [SQL Server]
- database monitoring [SQL Server], bottlenecks
- performance [SQL Server], bottlenecks
- tuning databases [SQL Server], bottlenecks
- monitoring server performance [SQL Server], bottlenecks
- monitoring performance [SQL Server], bottlenecks
- database performance [SQL Server], bottlenecks
- server performance [SQL Server], bottlenecks
- bottlenecks [SQL Server]
- identifying bottlenecks [SQL Server]
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bbabafa1f5b367343f02c3a0bf3e122bc827ce66
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67946759"
---
# <a name="identify-bottlenecks"></a>Individuare i colli di bottiglia
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In seguito all'accesso simultaneo alle risorse condivise si possono verificare colli di bottiglia. I colli di bottiglia in genere sono inevitabili e presenti in qualsiasi sistema software. È tuttavia necessario identificare e ottimizzare le situazioni di eccesso di domanda, in quanto una domanda eccessiva delle risorse condivise comporta un rallentamento dei tempi di risposta.  
  
 Le possibili cause dei colli di bottiglia sono:  
  
-   Risorse insufficienti che rendono necessari l'aggiunta di componenti o l'aggiornamento dei componenti disponibili.  
  
-   Carichi di lavoro non distribuiti equamente tra risorse dello stesso tipo, ad esempio monopolizzazione di un disco.  
  
-   Funzionamento non corretto delle risorse.  
  
-   Configurazione non corretta delle risorse.  
  
## <a name="analyzing-bottlenecks"></a>Analisi dei colli di bottiglia  
 La durata eccessiva di alcuni eventi segnala la presenza di colli di bottiglia che è possibile ottimizzare.  
  
 Ad esempio:  
  
-   È possibile che un altro componente impedisca che il processo di caricamento raggiunga il componente in uso, con un conseguente incremento dei tempi necessari per completare il caricamento.  
  
-   Le richieste client potrebbero richiedere tempi più lunghi a causa di traffico di rete intenso.  
  
 Per la valutazione delle prestazioni del server allo scopo di individuare eventuali colli di bottiglia, è necessario eseguire il monitoraggio delle cinque aree fondamentali descritte nella tabella seguente.  
  
|Possibile area in cui è presente un collo di bottiglia|Effetti sul server|  
|------------------------------|---------------------------|  
|Utilizzo della memoria|Se la memoria allocata per Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o disponibile per il sistema non è sufficiente, le prestazioni risultano inferiori. I dati infatti devono essere letti nel disco anziché direttamente nella cache dei dati. Microsoft Windows NT esegue un paging eccessivo con uno swapping dei dati da e nel disco in base alle pagine richieste.|  
|Uso della CPU|Se la frequenza di utilizzo della CPU risulta costantemente elevata, potrebbe essere necessario ottimizzare le query [!INCLUDE[tsql](../../includes/tsql-md.md)] o aggiornare la CPU.|  
|Input/output (I/O) del disco|[!INCLUDE[tsql](../../includes/tsql-md.md)] le query possono essere ottimizzate per ridurre le operazioni di I/O del disco non necessarie, ad esempio tramite l'uso di indici.|  
|Connessioni utente|Se il numero di utenti che accede al server simultaneamente è molto elevato, le prestazioni potrebbe risultare inferiori.|  
|Blocchi di blocco|L'utilizzo di applicazioni progettate in modo non corretto può causare blocchi e ostacolare la concorrenza, con un conseguente rallentamento dei tempi di risposta e una diminuzione della velocità effettiva.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo della CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Monitoraggio dell'utilizzo del disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Monitoraggio dell'utilizzo della memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [Oggetto Statistiche generali di SQL Server](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [Oggetto Locks di SQL Server](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  
