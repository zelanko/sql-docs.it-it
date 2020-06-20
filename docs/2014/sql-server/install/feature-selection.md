---
title: Selezione delle funzioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ec5bf4706f349a4e0aabb254b4ac74f9d396128d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065396"
---
# <a name="feature-selection"></a>Selezione caratteristiche
  Usare le caselle di controllo disponibili nella pagina **Selezione funzionalità** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per selezionare i componenti desiderati per la propria installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-ssnoversion-features"></a>Installazione delle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella pagina **Selezione funzionalità** , le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono separate in due sezioni principali: **Funzionalità istanza** e **Funzionalità condivise**.  
  
 **Funzionalità istanza** contiene i componenti che vengono installati una volta per ogni istanza e di cui saranno quindi presenti più copie (una per ogni istanza). Ogni istanza può essere una versione separata per cui è disponibile un livello di patch diverso. Quando si installa una patch, indipendentemente dal fatto che sia un Service Pack, un hotfix o un aggiornamento cumulativo, vengono aggiornati solo i file per un'istanza in un computer specifico e le funzionalità condivise, se non sono già state aggiornate.  
  
 **Funzionalità condivise** contiene le funzionalità comuni a tutte le istanze di un computer specifico. Ognuna di queste funzionalità condivise viene progettata per essere compatibile con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportate (Service Pack, aggiornamenti cumulativi e hotfix) che possono essere installate side-by-side.  
  
> [!NOTE]  
>  ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cluster di failover:** i [!INCLUDE[ssDE](../../includes/ssde-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] componenti e sono le uniche [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] funzionalità che supportano il clustering di failover. Sebbene sia possibile installare altri componenti, ad esempio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], in un nodo del cluster di failover, questi non sono compatibili e non viene eseguito il failover dei rispettivi servizi se il nodo del cluster di failover passa alla modalità offline. Per altre informazioni, vedere [Istanze del cluster di failover Always On &#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
### <a name="instance-features"></a>Funzionalità istanza  
 Quando si seleziona un gruppo di componenti, nel riquadro **Descrizione** verrà visualizzata la relativa descrizione. È possibile selezionare qualsiasi combinazione di caselle di controllo. Per continuare, è necessario effettuare una selezione.  
  
|Funzionalità|Descrizione|  
|--------------|-----------------|  
|Servizi[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]include [!INCLUDE[ssDE](../../includes/ssde-md.md)] , il servizio di base per l'archiviazione, l'elaborazione e la protezione dei dati, la replica, la ricerca full-text, gli strumenti per la gestione di dati XML e relazionali e il [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] Server (DQS). Le funzionalità del motore di database sono le seguenti:<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] è il servizio principale per l'archiviazione, l'elaborazione e la sicurezza dei dati.<br /><br /> Replica (facoltativo): la funzione di replica è costituita da un set di tecnologie per la copia e la distribuzione di dati e oggetti di database da un database a un altro e la successiva sincronizzazione dei database per garantirne la coerenza.<br /><br /> Ricerca full-text (facoltativa): la ricerca full-text fornisce le funzionalità necessarie per eseguire query full-text su semplici dati di tipo carattere in tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (facoltativo): [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) è una soluzione per la pulizia dei dati che consente di individuare dati incoerenti e non corretti nell'origine dati e che offre metodi computerizzati e interattivi per pulire i dati. Selezionare questa casella di controllo per installare il server DQS. Al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario eseguire il file DQSInstaller.exe per *completare* l'installazione del server DQS. Se è stata installata l'istanza predefinita di SQL Server, questo file è disponibile in c:\Programmi \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. MSSQLSERVER\MSSQL\Binn.<br /><br /> <br /><br /> ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cluster di failover:** i componenti di replica e di ricerca full-text sono necessari e vengono selezionati automaticamente dal programma di installazione per le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazioni del clustering di failover quando si seleziona motore di database Services.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include gli strumenti per la creazione e la gestione delle applicazioni di data mining e Online Analytical Processing (OLAP).|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Nativo|Nella modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono inclusi componenti client e server per la creazione, la gestione e la distribuzione di report tabulari, matrice, grafici e in formato libero. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è inoltre una piattaforma estendibile che consente di sviluppare applicazioni di creazione di report.|  
  
> [!IMPORTANT]
>  1.  Con il programma di installazione non è possibile configurare il bilanciamento del carico e l'indirizzamento a URL singolo per più nodi in una distribuzione con scalabilità orizzontale di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per completare una distribuzione con scalabilità orizzontale, è necessario utilizzare Windows Server, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center o un software di gestione cluster di terze parti. Per ulteriori informazioni sulla configurazione della distribuzione di Web farm, vedere la pagina relativa alla [configurazione di Reporting Services per la distribuzione con scalabilità orizzontale](https://go.microsoft.com/fwlink/?LinkId=199448) ( https://go.microsoft.com/fwlink/?LinkId=199448) .  
> 2.  Per informazioni sui requisiti a livello di browser dei componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Pianificazione per il supporto browser per Reporting Services e Power View &#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
> 3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è supportato in configurazioni side-by-side presenti contemporaneamente nella piattaforma a 64 bit e nel sottosistema a 32 bit (WOW64) di un server a 64 bit.  
  
### <a name="shared-features"></a>Funzionalità condivise  
 Le funzionalità condivise da tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un singolo computer vengono installate in un'unica directory. Essi includono quanto segue:  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]La modalità SharePoint è un'applicazione basata su server per la creazione, la gestione e il recapito di report alla posta elettronica, a più formati di file e a forme interattive basate sul Web. Nella modalità SharePoint la visualizzazione e la gestione dei report sono integrate nei prodotti SharePoint. Per altre informazioni, vedere [Server di report di Reporting Services &#40;modalità SharePoint&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md).|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - Componente aggiuntivo per prodotti SharePoint|Nel componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint sono disponibili componenti di gestione e dell'interfaccia utente che permettono di integrare un prodotto SharePoint con un server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint. Per ulteriori informazioni, vedere [la posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
|Client Data Quality|Il client Data Quality è un'applicazione autonoma che consente la connessione al server DQS e offre un'interfaccia utente grafica intuitiva per eseguire operazioni di pulizia o corrispondenza dei dati ed effettuare attività amministrative in DQS.|  
|Connettività strumenti client|Negli strumenti client sono inclusi i componenti per la comunicazione tra client e server, quali le librerie di rete per DB-Library, OLEDB per OLAP, ODBC, ADODB e ADOMD+.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un set di strumenti grafici e oggetti programmabili per lo spostamento, la copia e la trasformazione di dati.|  
|Compatibilità con le versioni precedenti di strumenti client.|In Compatibilità con le versioni precedenti di strumenti client sono inclusi i componenti seguenti:<br /><br /> SQL-DMO (SQL Distributed Management Objects). Per altre informazioni, vedere [Funzionalità di SQL Server obsolete in SQL Server 2014](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md).<br /><br /> DSO (Decision Support Objects). Per altre informazioni, vedere [Modifiche di rilievo nelle funzionalità di Analysis Services in SQL Server 2014](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md).|  
|SDK di strumenti client|È incluso il Software Development Kit (SDK) contenente le risorse per i programmatori.|  
|Componenti della documentazione|Nei componenti della documentazione sono inclusi i componenti per visualizzare e gestire il contenuto della Guida.|  
|Strumenti di gestione - Di base|**Strumenti di gestione-di base:** Sono inclusi gli elementi seguenti:<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]supporto per [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , l'utilità **SQLCMD** e il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider PowerShell<br /><br /> **Strumenti di gestione-completa:** Sono inclusi i componenti seguenti oltre ai componenti della versione di base:<br /><br /> Supporto di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Gestione utilità|  
|Controller di Riesecuzione distribuita|Con il controller di Riesecuzione distribuita è possibile orchestrare le azioni dei client Riesecuzione distribuita. In ogni ambiente di Riesecuzione distribuita può essere presente una sola istanza del controller. Per altre informazioni, vedere [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|Client Riesecuzione distribuita|I client Riesecuzione distribuita vengono utilizzati insieme per simulare carichi di lavoro in un'istanza di SQL Server. In ogni ambiente di Riesecuzione distribuita possono essere presenti uno o più client. Per altre informazioni, vedere [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|SDK di Connettività SQL Client|È incluso l'SDK di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) per lo sviluppo dell'applicazione di database.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] è una piattaforma per l'integrazione di dati da sistemi disparati di un'organizzazione in una sola origine di dati master per fini di accuratezza e controllo. Tramite l'opzione [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] vengono installati [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], assembly, uno snap-in di Windows PowerShell, nonché cartelle e file per servizi e applicazioni Web.|  
  
 Per impostazione predefinita, i componenti condivisi vengono installati in %ProgramFiles%\Microsoft SQL Server\\. Per modificare il percorso di installazione, fare clic sul pulsante **Sfoglia** . Se si modifica il percorso di installazione di un componente condiviso, la modifica verrà applicata a tutti gli altri componenti condivisi. Nelle installazioni successive i componenti condivisi verranno installati nello stesso percorso dell'installazione originale.  
  
 **Directory radice istanza** : per impostazione predefinita, la directory radice dell'istanza è c:\Programmi \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \\ . Per specificare una directory radice diversa da quella predefinita, fare clic sul pulsante **Sfoglia** oppure specificare un percorso.  
  
 Nei sistemi operativi basati su processore x64, è possibile specificare il percorso di installazione dei componenti 64 bit e quello dei componenti a 32 bit nel sottosistema WOW64.  
  
## <a name="disk-space-requirements"></a>Requisiti relativi allo spazio su disco  
 Utilizzare la pagina Riepilogo spazio richiesto per esaminare i requisiti di spazio su disco relativi alle funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionate per l'installazione.  
  
### <a name="options"></a>Opzioni  
 Se lo spazio su disco richiesto è troppo elevato, considerare le opzioni seguenti:  
  
-   Impostare le directory di installazione su un'unità con una quantità maggiore di spazio su disco.  
  
-   Modificare le caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'installazione.  
  
-   Creare più spazio disponibile nell'unità specificata spostando gli altri file o le altre applicazioni.  
  
## <a name="installing-adventureworks-sample-databases"></a>Installazione dei database di esempio AdventureWorks  
 Per impostazione predefinita, i database di esempio e il codice di esempio non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni sull'installazione di database di esempio e codice di esempio, vedere la [Microsoft SQL Server progetti della Community & esempi](https://go.microsoft.com/fwlink/?LinkId=87843) ( https://go.microsoft.com/fwlink/?LinkId=87843) .  
  
 Informazioni aggiuntive sugli esempi sono disponibili in seguito all'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Dal menu **Start** , scegliere **tutti i programmi**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** , **documentazione ed esercitazioni**e quindi fare clic su ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Panoramica esempi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Edizioni e componenti di SQL Server 2014](../editions-and-components-of-sql-server-2016.md)  
  
  
