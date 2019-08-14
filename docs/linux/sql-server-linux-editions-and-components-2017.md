---
title: Edizioni e funzionalità supportate di SQL Server 2017 ~ Linux
ms.date: 09/14/2017
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 249fb623945c1e086a677268d857f3bb16362a2e
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811194"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Edizioni e funzionalità supportate di SQL Server 2017 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo offre informazioni dettagliate sulle funzionalità supportate dalle diverse edizioni di SQL Server 2017 in Linux. Per le edizioni e le funzionalità supportate di SQL Server in Windows, vedere [ SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
I requisiti di installazione variano in base alle esigenze dell'applicazione. Le diverse edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consentono di soddisfare le esigenze specifiche di utenti e organizzazioni in termini di prezzo, esecuzione e prestazioni. I componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installati dipendono inoltre dai requisiti specifici. Nelle sezioni seguenti vengono fornite tutte le informazioni necessarie per adottare la scelta migliore tra le edizioni e i componenti disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Per le note sulla versione più recenti e informazioni sulle novità, vedere quanto segue:
- [Note sulla versione di SQL Server in Linux](sql-server-linux-release-notes.md)
- [Novità di SQL Server in Linux](sql-server-linux-whats-new.md)

Per l'elenco delle funzionalità di SQL Server non disponibili in Linux, vedere [Funzionalità e servizi non supportati](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Per provare SQL Server    
    
[Download di SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Edizioni di[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 La tabella seguente descrive tali edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|Edizione di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Definizione|  
|---------------------------------------|----------------|  
|Enterprise|L'offerta Premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition, offre le funzionalità complete dei centri dati di fascia alta con prestazioni velocissime, abilitando livelli di servizio elevati per carichi di lavoro di importanza critica.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard offre funzionalità di gestione dati di base per l'esecuzione di applicazioni per reparti e piccole organizzazioni e supporta gli strumenti di sviluppo comuni locali e per cloud, abilitando una gestione efficace del database con risorse IT minime.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition costituisce un'opzione con un costo totale di proprietà ridotto per provider di servizi di hosting Web e VAP Web, offrendo funzionalità di scalabilità, convenienza e facilità di gestione per proprietà Web di ogni dimensione.|  
|Developer|L'edizione[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer consente agli sviluppatori di compilare qualsiasi tipo di applicazione in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Benché includa tutte le funzionalità dell'edizione Enterprise, ne è consentito l'utilizzo solo come sistema di sviluppo e di prova e non come server di produzione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer rappresenta la scelta ideale per chi desidera compilare e testare applicazioni.|  
|Express edition|L'edizione Express è un database di base gratuito, ideale per l'apprendimento e la compilazione di applicazioni basate sui dati desktop e server di piccole dimensioni. Questa edizione costituisce la scelta ottimale per fornitori di software indipendenti, sviluppatori e sviluppatori amatoriali di applicazioni client. Se sono necessarie funzionalità di database più avanzate, è possibile aggiornare facilmente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express a versioni di fascia superiore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Uso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con applicazioni client/server  

È possibile installare solo i componenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un computer in cui vengono eseguite applicazioni client/server connesse direttamente a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'installazione di componenti client rappresenta una scelta ottimale anche se si amministra un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un server di database o se si prevede di sviluppare applicazioni basate su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>Componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  

SQL Server 2017 in Linux supporta il motore di database di SQL Server. La tabella seguente descrive le funzionalità del motore di database.   
  
|Componenti server|Descrizione|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] include il [!INCLUDE[ssDE](../includes/ssde-md.md)], il servizio principale per l'archiviazione, l'elaborazione e la protezione dei dati, la replica, la ricerca full-text, gli strumenti per la gestione di dati XML e relazionali e l'integrazione dell'analisi dei dati.|  

**Developer Edition, Enterprise Core Edition ed Evaluation Edition**  
Per le funzionalità supportate dalle edizioni Developer Edition, Enterprise Core Edition ed Evaluation Edition, vedere le funzionalità elencate per SQL Server Enterprise Edition nelle tabelle seguenti.

L'edizione Developer continua a supportare un solo client per la [riesecuzione distribuita di SQL Server](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Limiti di scalabilità  
  
|Funzionalità|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Capacità di calcolo massima usata da una singola istanza - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Valore massimo del sistema operativo|Limitato a meno di 4 socket o 24 core|Limitato a meno di 4 socket o 16 core|Limitato a meno di 1 socket o 4 core| 
|Capacità di calcolo massima usata da una singola istanza - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oppure [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Valore massimo del sistema operativo|Limitato a meno di 4 socket o 24 core|Limitato a meno di 4 socket o 16 core|Limitato a meno di 1 socket o 4 core|
|Memoria massima per il pool di buffer per ogni istanza di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|valore massimo del sistema operativo|128 GB|64 GB|1410 MB|
|Memoria massima per la cache dei segmenti Columnstore per ogni istanza di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria illimitata| 32 GB| 16 GB| 352 MB|  
|Dimensione massima dati ottimizzati per la memoria per ogni database in [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memoria illimitata| 32 GB| 16 GB| 352 MB|
|Dimensione massima del database relazionale|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> La licenza basata su Enterprise Edition con Server + Licenza CAL (Client Access License), non disponibile per nuovi contratti, è limitata a un massimo di 20 core per istanza di SQL Server. Non sono previsti limiti nel modello di licenza server basato su core. Per altre informazioni, vedere [Limiti della capacità di calcolo per edizione di SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Disponibilità elevata RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Log shipping|Sì|Sì|Sì|no|  
|Compressione backup|Sì|Sì|no|no| 
|Snapshot del database|Sì|no|no|no|
|Istanza del cluster di failover Always On<sup>1</sup>|Sì|Sì|no|no| 
|Gruppi di disponibilità AlwaysOn<sup>2</sup>|Sì|no|no|no|
|Gruppi di disponibilità di base<sup>3</sup>|no|Sì|no|no|
|Gruppo di disponibilità con commit di un numero minimo di repliche|Sì|Sì|no|no|
|Gruppo di disponibilità senza cluster|Sì|Sì|no|no|
|Ripristino di pagine e file online|Sì|no|no|no|
|Indicizzazione online|Sì|no|no|no|
|Ricompilazioni degli indici online ripristinabili|Sì|no|no|no|
|Modifica dello schema online|Sì|no|no|no|
|Recupero rapido|Sì|no|no|no|
|Backup con mirroring|Sì|no|no|no|
|Aggiunta di memoria a caldo e CPU|Sì|no|no|no|
|Backup crittografato|Sì|Sì|no|no|
|Backup ibrido in Microsoft Azure (backup nell'URL)|Sì|Sì|no|no|
  
<sup>1</sup> In Enterprise Edition il numero di nodi corrisponde al valore massimo del sistema operativo. In Standard Edition è presente il supporto per due nodi. 

<sup>2</sup> In Enterprise Edition è disponibile il supporto fino a 8 repliche secondarie, incluse 2 repliche secondarie sincrone. 

<sup>3</sup> Standard Edition supporta i gruppi di disponibilità di base. Un gruppo di disponibilità di base supporta due repliche, con un database. Per altre informazioni sui gruppi di disponibilità di base, vedere [Gruppi di disponibilità di base](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> Scalabilità e prestazioni RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|Sì|Sì|Sì|Sì|  
|File binari di oggetti di grandi dimensioni in indici columnstore cluster|Sì|Sì|Sì|Sì|  
|Ricompilazione degli indici columnstore non cluster online|Sì|no|no|no|
|OLTP in memoria <sup>1</sup>|Sì|Sì|Sì|Sì|
|Memoria principale persistente|Sì|Sì|Sì|Sì|
|Partizionamento di tabelle e indici|Sì|Sì|Sì|Sì|  
|Compressione dati|Sì|Sì|Sì|Sì|
|Resource Governor|Sì|no|no|no|  
|Parallelismo della tabella partizionata|Sì|no|no|no|
|Allocazione di una matrice di buffer e di memoria in pagine grandi con supporto NUMA|Sì|no|no|no|
|Governance delle risorse di I/O|Sì|no|no|no|  
|Durabilità posticipata|Sì|Sì|Sì|Sì|
|Ottimizzazione automatica|Sì|no|no|no|
|Join adattivi in modalità batch|Sì|no|no|no|
|Feedback delle concessioni di memoria in modalità batch|Sì|no|no|no|
|Esecuzione interleaved per funzioni con valori di tabella a più istruzioni|Sì|Sì|Sì|Sì|
|Miglioramenti dell'inserimento bulk|Sì|Sì|Sì|Sì|


<sup>1</sup> Le dimensioni dati OLTP in memoria e la cache dei segmenti Columnstore sono limitate alla quantità di memoria specificata dall'edizione nella sezione Limiti di scalabilità. I gradi di parallelismo (DOP) massimi sono limitati. I gradi di parallelismo del processo (DOP) per le compilazioni di indici sono limitati a 2 per Standard Edition e a 1 per le Web Edition ed Express Edition. Questo si riferisce agli indici columnstore creati tramite le tabelle basate su disco e le tabelle ottimizzate per la memoria.

##  <a name="RDBMSS"></a> Sicurezza RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Sicurezza a livello di riga|Sì|Sì|Sì|Sì|  
|Crittografia sempre attiva|Sì|Sì|Sì|Sì| 
|Mascheramento dati dinamici|Sì|Sì|Sì|Sì|   
|Controllo di base|Sì|Sì|Sì|Sì| 
|Controllo con granularità fine|Sì|Sì|Sì|Sì| 
|Crittografia trasparente del database|Sì|no|no|no|   
|Ruoli definiti dall'utente|Sì|Sì|Sì|Sì| 
|Database indipendenti|Sì|Sì|Sì|Sì| 
|Crittografia per backup|Sì|Sì|no|no|  

##  <a name="RDBMSM"></a> Gestione RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Connessione amministrativa dedicata|Sì|Sì|Sì|Sì, con flag di traccia|Sì, con flag di traccia|   
|Supporto per script di PowerShell|Sì|Sì|Sì|Sì| 
|Supporto per le operazioni del componente dell'applicazione livello dati (DAC) - estrazione, distribuzione, aggiornamento, eliminazione|Sì|Sì|Sì|Sì| 
|Automazione dei criteri (controllo pianificato e modifica)|Sì|Sì|Sì|no|no|   
|Agente di raccolta dati relativi alle prestazioni|Sì|Sì|Sì|no|no| 
|Report di prestazioni standard|Sì|Sì|Sì|no|no| 
|Guide di piano e blocco del piano per le guide di piano|Sì|Sì|Sì|no|no|   
|Query diretta di viste indicizzate (tramite hint NOEXPAND)|Sì|Sì|Sì|Sì| 
|Gestione automatica viste indicizzate|Sì|Sì|Sì|no|no| 
|Viste partizionate distribuite|Sì|no|no|no| 
|Operazioni indicizzate parallele|Sì|no|no|no|  
|Utilizzo automatico di viste indicizzate da Query Optimizer|Sì|no|no|no| 
|Verifica di coerenza parallela|Sì|no|no|no| 
|Punto di controllo dell'Utilità SQL Server|Sì|no|no|no|    

##  <a name="Programmability"></a> Programmability  
  
|Funzionalità|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Sì|Sì|Sì|Sì|   
|Archivio query|Sì|Sì|Sì|Sì|   
|Temporale|Sì|Sì|Sì|Sì|   
|Supporto XML nativo|Sì|Sì|Sì|Sì| 
|Indicizzazione XML|Sì|Sì|Sì|Sì| 
|Funzionalità MERGE e UPSERT|Sì|Sì|Sì|Sì|   
|Tipi di dati data e ora|Sì|Sì|Sì|Sì|  
|Supporto di internazionalizzazione|Sì|Sì|Sì|Sì| 
|Ricerca full-text e semantica|Sì|Sì|Sì|Sì|no| 
|Impostazione della lingua nelle query|Sì|Sì|Sì|Sì|no|   
|Service Broker (messaggistica)|Sì|Sì|No (solo client)|No (solo client)|No (solo client)|   
|Transact-SQL - endpoint|Sì|Sì|Sì|no|no| 
|Grafico|Sì|Sì|Sì|Sì|  


<sup>1</sup> La scalabilità orizzontale con più nodi di calcolo richiede un nodo head.

## <a name="IS"></a> Integration Services

Per informazioni sulle funzionalità di Integration Services (SSIS) supportate dalle edizioni di [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], vedere [Funzionalità di Integration Services supportate dalle edizioni di SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Servizi spaziali e basati sulla posizione  
  
|Nome funzionalità|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Indici spaziali|Sì|Sì|Sì|Sì|   
|Tipi di dati planari e geodetici|Sì|Sì|Sì|Sì| 
|Librerie spaziali avanzate|Sì|Sì|Sì|Sì|   
|Importazione/esportazione di formati di dati spaziali standard del settore|Sì|Sì|Sì|Sì|   

  
## <a name="next-steps"></a>Passaggi successivi 
 [Edizioni e funzionalità supportate per SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Edizioni e funzionalità supportate per SQL Server 2016 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Edizioni e funzionalità supportate per SQL Server 2014 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Installation for SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md) (Installazione per SQL Server)  
 [Documentazione di SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
