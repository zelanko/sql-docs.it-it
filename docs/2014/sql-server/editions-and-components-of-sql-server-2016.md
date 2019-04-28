---
title: Edizioni e componenti di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9610dc1cc729dc555d42c0dfe5eeb117f9cfba18
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806347"
---
# <a name="editions-and-components-of-sql-server-2014"></a>Edizioni e componenti di SQL Server 2014
  I requisiti di installazione variano in base alle esigenze dell'applicazione. Le diverse edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consentono di soddisfare le esigenze specifiche di utenti e organizzazioni in termini di prezzo, esecuzione e prestazioni. I componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installati dipendono inoltre dai requisiti specifici. Nelle sezioni seguenti vengono fornite tutte le informazioni necessarie per adottare la scelta migliore tra le edizioni e i componenti disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="principal-editions-of-includesscurrentincludessscurrent-mdmd"></a>Edizioni principali di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Nella tabella seguente vengono descritte le edizioni principali di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|Edizione di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Definizione|  
|---------------------------------------|----------------|  
|Enterprise (64 e 32 bit)|L'offerta Premium, [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise Edition offre le funzionalità complete dei centri dati di fascia alta con prestazioni velocissime, virtualizzazione illimitata e Business Intelligence end-to-end, abilitando livelli di servizio elevati per carichi di lavoro di importanza critica e l'accesso dell'utente finale per la comprensione dei dati.|  
|Business Intelligence (64 e 32 bit)|L'edizione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence offre una piattaforma completa consentendo alle organizzazioni di compilare e distribuire soluzioni BI sicure, scalabili e gestibili. Offre funzionalità eccezionali quali, ad esempio, l'esplorazione dei dati basata su browser, potenti funzionalità di mash-up dei dati e gestione di integrazione avanzata.|  
|Standard (64 e 32 bit)|L'edizione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard offre un database di gestione dati e di Business Intelligence di base per l'esecuzione di applicazioni per reparti e piccole organizzazioni e supporta gli strumenti di sviluppo comuni locali e per cloud, abilitando una gestione efficace del database con risorse IT minime.|  
  
## <a name="specialized-editions-of-includesscurrentincludessscurrent-mdmd"></a>Edizioni specializzate di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Le edizioni specializzate di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono destinate per i carichi di lavoro aziendali. Nella tabella seguente vengono descritte le edizioni specializzate di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Edizione di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Descrizione|  
|---------------------------------------|-----------------|  
|Web (64 e 32 bit)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web Edition costituisce un'opzione con un costo totale di proprietà ridotto per provider di servizi di hosting Web e VAP Web, offrendo funzionalità di scalabilità, convenienza e facilità di gestione per proprietà Web di ogni dimensione.|  
  
## <a name="breadth-editions-of-includesscurrentincludessscurrent-mdmd"></a>Edizioni Breadth di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Le edizioni Breadth di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono pianificate per scenari di clienti specifici e vengono offerte GRATIS o a un costo minimo. Nella tabella seguente vengono descritte le edizioni Breadth di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|Edizione di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Descrizione|  
|---------------------------------------|-----------------|  
|Developer (64 e 32 bit)|L'edizione[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer consente agli sviluppatori di compilare qualsiasi tipo di applicazione in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Benché includa tutte le funzionalità dell'edizione Enterprise, ne è consentito l'utilizzo solo come sistema di sviluppo e di prova e non come server di produzione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer rappresenta la scelta ideale per chi desidera compilare e testare applicazioni.|  
|Edizioni Express (64 e 32 bit)|L'edizione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express è un database di base gratuito, ideale per l'apprendimento e la compilazione di applicazioni basate sui dati desktop e server di piccole dimensioni. Questa edizione costituisce la scelta ottimale per fornitori di software indipendenti, sviluppatori e sviluppatori amatoriali di applicazioni client. Se sono necessarie funzionalità di database più avanzate, è possibile aggiornare facilmente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express a versioni di fascia superiore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB, una versione leggera di Express che, pur includendone tutte le funzionalità di programmazione, viene eseguita in modalità utente e prevede un'installazione veloce senza operazioni di configurazione, nonché un elenco ridotto di prerequisiti.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>Utilizzo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con un server Internet  
 In un server Internet, ad esempio un server in cui viene eseguito Internet Information Services (IIS), vengono in genere installati gli strumenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Gli strumenti client includono i componenti di connettività client utilizzati dalle applicazioni per la connessione a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Benché sia possibile installare un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nello stesso computer in cui è in esecuzione IIS, si tratta in genere di una configurazione utilizzata solo per siti Web di piccole dimensioni che dispongono di un singolo computer server. Nella maggior parte dei siti Web, i sistemi IIS di livello intermedio risiedono in un server o in un cluster di server, mentre i database corrispondenti si trovano in un server separato o in una federazione di server.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Utilizzo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con applicazioni client/server  
 È possibile installare solo i componenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un computer in cui vengono eseguite applicazioni client/server connesse direttamente a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. L'installazione di componenti client rappresenta una scelta ottimale anche se si amministra un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un server di database o se si prevede di sviluppare applicazioni basate su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 La scelta degli strumenti client comporta l'installazione delle seguenti funzionalità [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : componenti per la compatibilità con le versioni precedenti, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], componenti di connettività, strumenti di gestione, Software Development Kit e componenti della documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>Scelta tra i componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Per selezionare i componenti da includere in un'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , utilizzare la pagina di selezione delle funzionalità dell'Installazione guidata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per impostazione predefinita, non è selezionata alcuna funzionalità inclusa nell'albero.  
  
 Utilizzare le informazioni incluse nelle tabelle seguenti per determinare il set di funzionalità più adatto per le proprie esigenze.  
  
|Componenti server|Descrizione|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] include il [!INCLUDE[ssDE](../includes/ssde-md.md)], il servizio principale per l'archiviazione, elaborazione e la protezione dei dati, replica, ricerca full-text, strumenti per la gestione relazionali e dati XML e il [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] server (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] include gli strumenti per la creazione e la gestione delle applicazioni di data mining e Online Analytical Processing (OLAP).|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|In[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sono inclusi componenti client e server per la creazione, la gestione e la distribuzione di report tabulari, matrice, grafici e in formato libero. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è inoltre una piattaforma estendibile che consente di sviluppare applicazioni di creazione di report.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è un set di strumenti grafici e oggetti programmabili per lo spostamento, la copia e la trasformazione di dati. È incluso, inoltre, il componente [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) per [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) è la soluzione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la gestione dei dati master. MDS può essere configurato per gestire qualsiasi dominio (prodotti, clienti, account) e può includere gerarchie, sicurezza granulare, transazioni, controllo delle versioni dei dati e regole business e un [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] che può essere utilizzato per gestire dati.|  
  
|Strumenti di gestione|Descrizione|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è un ambiente integrato per l'accesso, la configurazione, la gestione, l'amministrazione e lo sviluppo di componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] consente a sviluppatori e amministratori con qualsiasi livello di esperienza di utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gestione configurazione|Gestione configurazione[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] offre funzionalità di base per la gestione della configurazione dei servizi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , dei protocolli server, dei protocolli client e degli alias per i client.|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] offre un'interfaccia utente grafica per il monitoraggio di un'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)] o di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|Ottimizzazione guidata[!INCLUDE[ssDE](../includes/ssde-md.md)] |Ottimizzazione guidata[!INCLUDE[ssDE](../includes/ssde-md.md)] consente di creare set di indici, viste indicizzate e partizioni ottimali.|  
|Client Data Quality|Fornisce un'interfaccia utente grafica estremamente intuitiva e semplice per la connessione al server DQS e per eseguire operazioni di pulizia dei dati. Consente inoltre di monitorare centralmente le varie attività eseguite durante l'operazione di pulizia dei dati.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|In[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] è disponibile un IDE per la compilazione di soluzioni per i componenti di Business Intelligence: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (in precedenza denominato Business Intelligence Development Studio).<br /><br /> In[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] è inoltre incluso un ambiente integrato che consente agli sviluppatori di database di svolgere tutte le attività di progettazione di database per qualsiasi piattaforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , locale e non, all'interno di Visual Studio. Gli sviluppatori di database possono utilizzare le funzionalità avanzate di Esplora server in Visual Studio per creare o modificare facilmente dati e oggetti di database oppure eseguire query.|  
|Componenti di connettività|Consente di installare i componenti per la comunicazione tra client e server nonché le librerie di rete per DB-Library, ODBC e OLE DB.|  
  
|Documentazione|Descrizione|  
|-------------------|-----------------|  
|Documentazione online di[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Documentazione principale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](install/planning-a-sql-server-installation.md)   
 [Installare SQL Server 2014 dall'installazione guidata di &#40;programma di installazione&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
