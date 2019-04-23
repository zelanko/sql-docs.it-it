---
title: Avvio rapido di installazione di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b06f5248152f8a11bf3e46d222df457f5442b6b4
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157247"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>Guida introduttiva all'installazione di SQL Server 2014
    
## <a name="introduction"></a>Introduzione  
 L'Installazione guidata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è basata su Windows Installer e dispone di un singolo albero delle funzionalità per l'installazione dei componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seguenti:  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   Strumenti di gestione  
  
-   Componenti di connettività  
  
 È possibile installare singolarmente ogni componente o selezionare una combinazione dei componenti elencati sopra. Per adottare la scelta migliore tra le edizioni e componenti disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], vedere [edizioni e componenti di SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è disponibile nelle edizioni a 32 bit e a 64 bit. Nell'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono supportate le seguenti opzioni di installazione:  
  
-   **Installazione guidata**  
  
     Vedere [installare SQL Server 2014 dall'installazione guidata di &#40;installazione&#41; ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) per istruzioni sull'installazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando l'installazione guidata.  
  
-   **Prompt dei comandi**  
  
     Visualizzare [installare SQL Server 2014 dal Prompt dei comandi](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) per esempio la sintassi e parametri di installazione per l'esecuzione dell'installazione automatica.  
  
-   **File di configurazione**  
  
     Visualizzare [installare SQL Server 2014 tramite un File di configurazione](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md) per esempio la sintassi e parametri di installazione per l'esecuzione il programma di installazione tramite un file di configurazione.  
  
-   **SysPrep**  
  
     Visualizzare [installare SQL Server 2014 tramite SysPrep](../database-engine/install-windows/install-sql-server-using-sysprep.md) per istruzioni sull'installazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando SysPrep.  
  
-   **Installazione Server Core**  
  
     Visualizzare [installare SQL Server 2014 in Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md) per istruzioni sull'installazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Windows Server Core.  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Installazione delle funzionalità di Business Intelligence**  
  
     Visualizzare [le funzionalità di BI di installare SQL Server 2014](../sql-server/install/install-sql-server-business-intelligence-features.md) per informazioni sull'installazione delle funzionalità che fanno parte della piattaforma Microsoft BI, che includono [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e diversi applicazioni client utilizzate per la creazione o l'utilizzo con i dati analitici.  
  
-   **Installazione del cluster di failover**  
  
     Visualizzare [installazione Cluster di Failover di SQL Server](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md) per istruzioni sull'installazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] su un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cluster di failover.  
  
 Per impostazione predefinita, i database di esempio e il codice di esempio non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per installare i database di esempio e il codice di esempio per le edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] diverse da Express, vedere il [sito Web CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Per informazioni sul supporto per il codice e i database di esempio di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], vedere [Panoramica di database ed esempi](https://go.microsoft.com/fwlink/?LinkId=110391).  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>Installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Indipendentemente dal fatto che si scelga di utilizzare l'Installazione guidata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o il prompt dei comandi per installare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il programma di istallazione prevede i passaggi seguenti.  
  
-   Esaminare i requisiti di installazione, i controlli di configurazione del sistema e le considerazioni sulla sicurezza per un'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  Per altre informazioni, vedere [Planning a SQL Server Installation](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall).  
  
-   Eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per aggiornare una versione esistente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per altre informazioni, vedere [l'aggiornamento a SQL Server 2014](#BKMK_Upgrading).  
  
-   Eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per installare una nuova istanza di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per altre informazioni, vedere [installazione di SQL Server 2014](#BKMK_Install).  
  
-   Una volta completata l'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], il successivo passaggio principale è la configurazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e dei relativi componenti. Utilizzare le utilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [configurazione di SQL Server 2014](#BKMK_Configure).  
  
 È possibile trovare spiegazioni dettagliate di queste attività nella sezione successiva.  
  
## <a name="related-tasks"></a>Attività correlate  
  
###  <a name="BKMK_BeforeYouInstall"></a> Pianificazione di un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installazione  
 Prima di installare [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], è necessario rivedere i requisiti hardware e software, le considerazioni sulla rete e Internet e le considerazioni sulla sicurezza per installare ed eseguire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [pianificazione di un'installazione di SQL Server](../../2014/sql-server/install/planning-a-sql-server-installation.md) e anche gli argomenti seguenti:  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Rivedere i requisiti hardware e software, le considerazioni sul supporto del sistema operativo, sulla rete e Internet e i requisiti di spazio libero su disco rigido.|[Prerequisiti di installazione](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|Esaminare le considerazioni sulla sicurezza per un'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Considerazioni sulla sicurezza](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|Rivedere i dettagli delle funzionalità supportate dalle diverse edizioni di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Edizioni e funzionalità](features-supported-by-the-editions-of-sql-server-2014.md)|  
|Determinare la scelta migliore tra le edizioni e i componenti disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Edizioni e componenti di SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|Rivedere la configurazione hardware e apprendere come preparare l'installazione del cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Operazioni preliminari all'installazione del clustering di failover](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a> L'aggiornamento a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 È possibile aggiornare le istanze esistenti di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per altre informazioni, vedere [esegue l'aggiornamento a SQL Server 2014](../database-engine/install-windows/upgrade-sql-server.md). Prima di avviare il programma di installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], vedere gli argomenti seguenti relativi al processo di aggiornamento:  
  
|Descrizione|Argomento|  
|-----------------|-----------|  
|Vengono indicati i percorsi di aggiornamento supportati da [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Aggiornamenti supportati](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|Viene descritto lo strumento Preparazione aggiornamento, con cui analizzare le istanze di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] per identificare i problemi di aggiornamento noti.|[Usare la Preparazione aggiornamento per preparare gli aggiornamenti](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|Viene descritta l'utilità Riesecuzione distribuita che consente di utilizzare più computer per riprodurre dati di traccia, simulando un carico di lavoro critico. Eseguendo una riproduzione in un server di prova prima e dopo un aggiornamento di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è possibile rilevare le differenze di prestazioni e individuare eventuali incompatibilità dell'applicazione con l'aggiornamento.|[Usare l'utilità Riesecuzione distribuita per preparare gli aggiornamenti](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|Vengono elencate le modifiche significative che potrebbero interessare le applicazioni in seguito all'aggiornamento a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Compatibilità con le versioni precedenti](backward-compatibility.md)|  
|Argomento contenente le procedure per aggiornare un'istanza autonoma di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata di &#40;programma di installazione&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|L'argomento contenente le procedure per aggiornare un'edizione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ad un'altra edizione. Per informazioni sui percorsi di aggiornamento supportati, vedere [Aggiornamenti di versione ed edizione supportati](../database-engine/install-windows/supported-version-and-edition-upgrades.md).|[Eseguire l'aggiornamento a un'edizione diversa di SQL Server 2014 &#40;programma di installazione&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta l'aggiornamento separato del [!INCLUDE[ssDE](../includes/ssde-md.md)] e di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dai cluster di failover [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ai cluster di failover di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] su tutti i nodi del cluster di failover. Per ulteriori informazioni, vedere questo argomento.|[Aggiornare un cluster di failover di SQL Server](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a> Installazione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Per informazioni sui vari scenari di installazione per [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], vedere gli argomenti seguenti.  
  
|Descrizione|Argomento|  
|-----------------|-----------|  
|Vengono forniti i collegamenti agli argomenti relativi all'installazione di vari componenti di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e agli argomenti contenenti la procedura per l'installazione di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Installare SQL Server 2014](../database-engine/install-windows/install-sql-server.md)|  
|Vedere questo argomento per installare [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] in Windows Server Core.|[Installare SQL Server 2014 in Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|Vedere questo argomento per aggiungere funzionalità a un'istanza esistente di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|[Aggiungere funzionalità a un'istanza di SQL Server 2014 &#40;programma di installazione&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|Rivedere questo argomento per creare una nuova istanza del cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Utilizzare questo argomento per gestire i nodi in un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esistente.|[Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Utilizzare questo argomento per installare gli strumenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un cluster di failover.|[Installare strumenti client in un cluster di failover di SQL Server](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|Esaminare l'utilizzo del report SQL Discovery per verificare la versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e le funzionalità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installate nel computer.|[Convalidare un'installazione di SQL Server](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|Vengono forniti i collegamenti agli argomenti sulle procedure per installare [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] tramite l'Installazione guidata, il prompt dei comandi, i file di configurazione e SysPrep.|[Procedure per l'installazione](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>Contenuto correlato  
 In questa sezione vengono fornite informazioni sulla configurazione e sulla disinstallazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_Configure"></a> La configurazione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Al termine dell'installazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è possibile configurare ulteriormente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tramite strumenti grafici e utilità del prompt dei comandi. Vedere gli argomenti seguenti per configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la prima volta:  
  
|Descrizione|Argomento|  
|-----------------|-----------|  
|Le informazioni fornite in questo argomento consentono di stabilire se è necessario sbloccare le porte di un firewall per consentire l'accesso ad [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o PowerPivot per SharePoint. Le procedure descritte consentono di configurare le impostazioni sia delle porte che del firewall.|[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|In questo argomento viene fornita una panoramica della configurazione del firewall e vengono riepilogate le informazioni utili a un amministratore di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|[Configurare Windows Firewall per consentire l'accesso a SQL Server](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|In questo argomento viene descritto come configurare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e Windows Firewall con sicurezza avanzata per fornire le connessioni di rete a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in un ambiente multihomed.|[Configurare un computer multihomed per l'accesso a SQL Server](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a> La disinstallazione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Negli argomenti seguenti viene descritto come disinstallare manualmente un'istanza autonoma e un'istanza cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
|Descrizione|Argomento|  
|-----------------|-----------|  
|In questo argomento viene descritto come disinstallare manualmente un'istanza autonoma di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Disinstallare SQL Server 2014](../sql-server/install/uninstall-sql-server.md)|  
|In questo argomento viene descritto come disinstallare un'istanza cluster di failover di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Rimuovere un'istanza del cluster di failover di SQL Server &#40;programma di installazione&#41;](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|In questo argomento vengono fornite informazioni sulla rimozione manuale di oggetti [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) dopo avere disinstallato [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o solo il server DQS.|[Rimuovere oggetti server Data Quality Services](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Specifiche di prodotto per SQL Server 2014](sql-server-2014-product-specifications.md)   
 [Introduzione a documentazione del prodotto per SQL Server](../2014-toc/books-online-for-sql-server-2014.md) [compatibilità con le versioni precedenti](backward-compatibility.md)  
  
  
