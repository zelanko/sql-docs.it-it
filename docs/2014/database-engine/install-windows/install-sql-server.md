---
title: Installare SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ed522c64e0f9652e3ffb310f98348c402193ef8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889248"
---
# <a name="install-sql-server-2014"></a>Installare SQL Server 2014
## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[Scarica SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Grazie a [Scott Hansel](http://www.hanselman.com/) per la raccolta di tutti i collegamenti al pacchetto di installazione in un'unica posizione.**
  
 In questo argomento è contenuta una panoramica delle diverse opzioni disponibili per l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per ulteriori informazioni sui vari [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componenti che possono essere installati e sul processo di installazione, vedere [installazione per SQL Server 2014](installation-for-sql-server.md).  
> **Nota:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile nelle edizioni a 32 bit e a 64 bit. Le edizioni a 64 bit e a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installate tramite l'Installazione guidata o il prompt dei comandi. Per ulteriori informazioni sui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componenti di, vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Per impostazione predefinita, i database di esempio e il codice di esempio non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per installare i database di esempio e il codice di esempio per le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diverse da Express, vedere il [sito Web CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Per informazioni sul supporto per il codice e i database di esempio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], vedere [Panoramica di database ed esempi](https://go.microsoft.com/fwlink/?LinkId=110391).  
  
 Prima di installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esaminare i requisiti di installazione, i controlli di configurazione di sistema e considerazioni sulla sicurezza. Per altre informazioni, vedere [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md). Per informazioni sui vari scenari di installazione per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere gli argomenti nella sezione successiva.  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>Installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] i componenti  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Informazioni sul Motore di database di SQL Server](../sql-server-database-engine-overview.md)|Viene descritto come installare e configurare il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Installare la replica di SQL Server](install-sql-server-replication.md)|Viene descritto come installare e configurare la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Installare Riesecuzione distribuita](../../tools/distributed-replay/install-distributed-replay-overview.md)|Vengono elencati gli argomenti sull'installazione della funzionalità Riesecuzione distribuita.|  
|[Installare gli strumenti di gestione di SQL Server](../../sql-server/install/install-sql-server-management-tools.md)|Viene descritto come installare e configurare gli strumenti di gestione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Installare SQL Server PowerShell](install-sql-server-powershell.md)|Vengono fornite considerazioni per l'installazione dei componenti di PowerShell per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>Come installare[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Procedure per l'installazione](../../sql-server/install/installation-how-to-topics.md)|Vengono forniti i collegamenti agli argomenti sulle procedure per installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite l'Installazione guidata, il prompt dei comandi, i file di configurazione e SysPrep.|  
|[Installare SQL Server 2014 in Server Core](install-sql-server-on-server-core.md)|Vedere questo argomento per installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in Windows Server Core.|  
|[Convalidare un'installazione di SQL Server](validate-a-sql-server-installation.md)|Esaminare l'utilizzo del report SQL Discovery per verificare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installate nel computer.|  
|[Parametri di controllo di Controllo configurazione sistema](check-parameters-for-the-system-configuration-checker.md)|Descrive la funzione di controllo configurazione sistema (SCC).|  
  
## <a name="configuration"></a>Configurazione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|In questo argomento viene fornita una panoramica della configurazione dei firewall e viene illustrato come configurare Windows Firewall.|  
|[Configurare un computer multihomed per l'accesso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|In questo argomento viene descritto come configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows Firewall con sicurezza avanzata per fornire le connessioni di rete a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente multihomed.|  
|[Configurare Windows Firewall per consentire l'accesso ad Analysis Services](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|Le procedure fornite in questo argomento consentono di configurare le impostazioni di porte e firewall necessarie per accedere ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o PowerPivot per SharePoint.|  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Installare SQL Server funzionalità BI di 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 Le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che fanno parte della piattaforma di Business Intelligence di [!INCLUDE[msCoName](../../includes/msconame-md.md)] includono [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] e diverse applicazioni client utilizzate per la creazione o l'utilizzo di dati analitici. In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene descritto come installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Installazione del cluster di failover di SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono descritte le modalità di installazione e configurazione del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Eseguire l'aggiornamento a SQL Server 2014](upgrade-sql-server.md)   
 [Disinstalla SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
