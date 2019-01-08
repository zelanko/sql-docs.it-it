---
title: Edizioni e funzionalità supportate di SQL Server 2017 ~ Linux | Microsoft Docs
ms.custom: sql-linux
ms.date: 09/14/2017
ms.prod: sql
ms.reviewer: ''
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
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 07aae4f4e619e38d41cd16a08e1e8f7267f5ed29
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533564"
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>Edizioni e funzionalità supportate di SQL Server 2017 in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo fornisce informazioni dettagliate sulle funzionalità supportate dalle varie edizioni di SQL Server 2017 in Linux. Per le edizioni e funzionalità supportate di SQL Server in Windows, vedere [SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md).  
  
I requisiti di installazione variano in base alle esigenze dell'applicazione. Le diverse edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consentono di soddisfare le esigenze specifiche di utenti e organizzazioni in termini di prezzo, esecuzione e prestazioni. I componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installati dipendono inoltre dai requisiti specifici. Nelle sezioni seguenti vengono fornite tutte le informazioni necessarie per adottare la scelta migliore tra le edizioni e i componenti disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Per le note sulla versione più recenti e informazioni sulle novità, vedere quanto segue:
- [Note sulla versione di SQL Server in Linux](sql-server-linux-release-notes.md)
- [Che cosa sono le novità di SQL Server in Linux](sql-server-linux-whats-new.md)

Per un elenco delle funzionalità di SQL Server non è disponibile in Linux, vedere [funzionalità non supportate e i servizi](sql-server-linux-release-notes.md#Unsupported).

### <a name="try-sql-server"></a>Per provare SQL Server    
    
[Scaricare SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Edizioni di[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]   
 La tabella seguente descrive tali edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|Edizione di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Definizione|  
|---------------------------------------|----------------|  
|Enterprise|L'offerta premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise edition offre funzionalità complete di datacenter fascia alta con prestazioni velocissime, abilitando livelli di servizio elevati per carichi di lavoro di importanza strategica.|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition offre gestione di dati di base per i reparti e piccole organizzazioni di eseguire le applicazioni e supporta gli strumenti di sviluppo comuni locali e cloud, abilitando una gestione efficace del database con risorse IT minime.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition costituisce un'opzione con un costo totale di proprietà ridotto per provider di servizi di hosting Web e VAP Web, offrendo funzionalità di scalabilità, convenienza e facilità di gestione per proprietà Web di ogni dimensione.|  
|Developer|L'edizione[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer consente agli sviluppatori di compilare qualsiasi tipo di applicazione in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Benché includa tutte le funzionalità dell'edizione Enterprise, ne è consentito l'utilizzo solo come sistema di sviluppo e di prova e non come server di produzione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer rappresenta la scelta ideale per chi desidera compilare e testare applicazioni.|  
|Express edition|L'edizione Express è un database di base gratuito, ideale per l'apprendimento e la compilazione di applicazioni basate sui dati desktop e server di piccole dimensioni. Questa edizione costituisce la scelta ottimale per fornitori di software indipendenti, sviluppatori e sviluppatori amatoriali di applicazioni client. Se sono necessarie funzionalità di database più avanzate, è possibile aggiornare facilmente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express a versioni di fascia superiore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Uso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con applicazioni client/server  

È possibile installare solo i componenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un computer in cui vengono eseguite applicazioni client/server connesse direttamente a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'installazione di componenti client rappresenta una scelta ottimale anche se si amministra un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un server di database o se si prevede di sviluppare applicazioni basate su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>Componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  

SQL Server 2017 in Linux supporta il motore di database di SQL Server. Nella tabella seguente vengono descritte le funzionalità nel motore di database.   
  
|Componenti server|Descrizione|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] include il [!INCLUDE[ssDE](../includes/ssde-md.md)], il servizio principale per l'archiviazione, elaborazione e la protezione dei dati, replica, ricerca full-text, strumenti per la gestione relazionali e dati XML e in integrazione analitica di database.|  

**Edizioni Developer, Enterprise Core e valutazione**  
Per le funzionalità supportate dalle, Enterprise Core, edizioni Developer ed Evaluation, vedere le funzionalità elencate per SQL Server Enterprise edition nelle tabelle seguenti.

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
  
<sup>1</sup> Enterprise edition con Server + CAL Client Access License () basati su licenza (non disponibile per nuovi contratti) è limitata a un massimo di 20 core per istanza di SQL Server. Non sono previsti limiti nel modello di licenza server basato su core. Per altre informazioni, vedere [limiti di capacità di calcolo per edizione di SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Disponibilità elevata RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Log shipping|Yes|Yes|Yes|No|  
|Compressione backup|Yes|Yes|No|No| 
|Snapshot del database|Yes|No|No|No|
|Always On istanza del cluster di failover<sup>1</sup>|Yes|Yes|No|No| 
|I gruppi di disponibilità Always On<sup>2</sup>|Yes|No|No|No|
|I gruppi di disponibilità di base <sup>3</sup>|No|Yes|No|No|
|Gruppo di disponibilità con commit di un numero minimo di repliche|Yes|Yes|No|No|
|Gruppo di disponibilità senza cluster|Yes|Yes|No|No|
|Ripristino di pagine e file online|Yes|No|No|No|
|Indicizzazione online|Yes|No|No|No|
|Ricompilazioni degli indici online ripristinabili|Yes|No|No|No|
|Modifica dello schema online|Yes|No|No|No|
|Recupero rapido|Yes|No|No|No|
|Backup con mirroring|Yes|No|No|No|
|Aggiunta di memoria a caldo e CPU|Yes|No|No|No|
|Backup crittografato|Yes|Yes|No|No|
|Backup ibrido in Microsoft Azure (backup nell'URL)|Yes|Yes|No|No|
  
<sup>1</sup> su Enterprise edition, il numero di nodi è il valore massimo del sistema operativo. In Standard Edition è presente il supporto per due nodi. 

<sup>2</sup> su Enterprise edition, fornisce il supporto per fino a 8 repliche secondarie, incluse 2 repliche secondarie sincrone. 

<sup>3</sup> standard edition supporta i gruppi di disponibilità di base. Un gruppo di disponibilità di base supporta due repliche, con un database. Per altre informazioni sui gruppi di disponibilità di base, vedere [Gruppi di disponibilità di base](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="RDBMSSP"></a> Scalabilità e prestazioni RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|Yes|Yes|Yes|Yes|  
|File binari di oggetti di grandi dimensioni in indici columnstore cluster|Yes|Yes|Yes|Yes|  
|Ricompilazione degli indici columnstore non cluster online|Yes|No|No|No|
|OLTP in memoria <sup>1</sup>|Yes|Yes|Yes|Yes|
|Memoria principale persistente|Yes|Yes|Yes|Yes|
|Partizionamento di tabelle e indici|Yes|Yes|Yes|Yes|  
|Compressione dati|Yes|Yes|Yes|Yes|
|Resource Governor|Yes|No|No|No|  
|Parallelismo della tabella partizionata|Yes|No|No|No|
|Allocazione di una matrice di buffer e di memoria in pagine grandi con supporto NUMA|Yes|No|No|No|
|Governance delle risorse di I/O|Yes|No|No|No|  
|Durabilità posticipata|Yes|Yes|Yes|Yes|
|Ottimizzazione automatica|Yes|No|No|No|
|Join adattivi in modalità batch|Yes|No|No|No|
|Feedback delle concessioni di memoria in modalità batch|Yes|No|No|No|
|Esecuzione interleaved per funzioni con valori di tabella a più istruzioni|Yes|Yes|Yes|Yes|
|Miglioramenti dell'inserimento bulk|Yes|Yes|Yes|Yes|


<sup>1</sup> Le dimensioni dati OLTP in memoria e la cache dei segmenti Columnstore sono limitate alla quantità di memoria specificata dall'edizione nella sezione Limiti di scalabilità. I gradi di parallelismo (DOP) massimi sono limitati. I gradi di parallelismo del processo (DOP) per la compilazione di un indice è limitato a 2 DOP per l'edizione Standard e 1 DOP per le edizioni Web ed Express. Questo si riferisce agli indici columnstore creati tramite le tabelle basate su disco e le tabelle ottimizzate per la memoria.

##  <a name="RDBMSS"></a> Sicurezza RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Sicurezza a livello di riga|Yes|Yes|Yes|Yes|  
|Crittografia sempre attiva|Yes|Yes|Yes|Yes| 
|Mascheramento dati dinamici|Yes|Yes|Yes|Yes|   
|Controllo di base|Yes|Yes|Yes|Yes| 
|Controllo con granularità fine|Yes|Yes|Yes|Yes| 
|Crittografia trasparente del database|Yes|No|No|No|   
|Ruoli definiti dall'utente|Yes|Yes|Yes|Yes| 
|Database indipendenti|Yes|Yes|Yes|Yes| 
|Crittografia per backup|Yes|Yes|No|No|  

##  <a name="RDBMSM"></a> Gestione RDBMS  
  
|Funzionalità|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Connessione amministrativa dedicata|Yes|Yes|Yes|Sì, con flag di traccia|Sì, con flag di traccia|   
|Supporto per script di PowerShell|Yes|Yes|Yes|Yes| 
|Supporto per le operazioni del componente dell'applicazione livello dati (DAC) - estrazione, distribuzione, aggiornamento, eliminazione|Yes|Yes|Yes|Yes| 
|Automazione dei criteri (controllo pianificato e modifica)|Yes|Yes|Yes|No|No|   
|Agente di raccolta dati relativi alle prestazioni|Yes|Yes|Yes|No|No| 
|Report di prestazioni standard|Yes|Yes|Yes|No|No| 
|Guide di piano e blocco del piano per le guide di piano|Yes|Yes|Yes|No|No|   
|Query diretta di viste indicizzate (tramite hint NOEXPAND)|Yes|Yes|Yes|Yes| 
|Gestione automatica viste indicizzate|Yes|Yes|Yes|No|No| 
|Viste partizionate distribuite|Yes|No|No|No| 
|Operazioni indicizzate parallele|Yes|No|No|No|  
|Utilizzo automatico di viste indicizzate da Query Optimizer|Yes|No|No|No| 
|Verifica di coerenza parallela|Yes|No|No|No| 
|Punto di controllo dell'Utilità SQL Server|Yes|No|No|No|    

##  <a name="Programmability"></a> Programmability  
  
|Funzionalità|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Yes|Yes|Yes|Yes|   
|Archivio query|Yes|Yes|Yes|Yes|   
|Temporale|Yes|Yes|Yes|Yes|   
|Supporto XML nativo|Yes|Yes|Yes|Yes| 
|Indicizzazione XML|Yes|Yes|Yes|Yes| 
|Funzionalità MERGE e UPSERT|Yes|Yes|Yes|Yes|   
|Tipi di dati data e ora|Yes|Yes|Yes|Yes|  
|Supporto di internazionalizzazione|Yes|Yes|Yes|Yes| 
|Ricerca full-text e semantica|Yes|Yes|Yes|Yes|No| 
|Impostazione della lingua nelle query|Yes|Yes|Yes|Yes|No|   
|Service Broker (messaggistica)|Yes|Yes|No (solo client)|No (solo client)|No (solo client)|   
|Transact-SQL - endpoint|Yes|Yes|Yes|No|No| 
|Grafico|Yes|Yes|Yes|Yes|  


<sup>1</sup> La scalabilità orizzontale con più nodi di calcolo richiede un nodo head.

## <a name="IS"></a> Integration Services

Per informazioni sulle funzionalità di Integration Services (SSIS) supportate dalle edizioni di [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], vedere [funzionalità di Integration Services supportate dalle edizioni di SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="SLS"></a> Servizi spaziali e basati sulla posizione  
  
|Nome funzionalità|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Indici spaziali|Yes|Yes|Yes|Yes|   
|Tipi di dati planari e geodetici|Yes|Yes|Yes|Yes| 
|Librerie spaziali avanzate|Yes|Yes|Yes|Yes|   
|Importazione/esportazione di formati di dati spaziali standard del settore|Yes|Yes|Yes|Yes|   

  
## <a name="next-steps"></a>Passaggi successivi 
 [Edizioni e funzionalità supportate per SQL Server 2017 - Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Edizioni e funzionalità supportate per SQL Server 2016 - Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Edizioni e funzionalità supportate per SQL Server 2014 - Windows](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [Installation for SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md) (Installazione per SQL Server)  
 [Specifiche di prodotto per SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
