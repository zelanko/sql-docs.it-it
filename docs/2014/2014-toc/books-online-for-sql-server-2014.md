---
title: Documentazione online di SQL Server 2014 | Microsoft Docs
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.technology: release-landing
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql12.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a943685156ce9ec0ed3c94f4650c5a8222bff445
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688778"
---
# <a name="books-online-for-sql-server-2014"></a>Books Online for SQL Server 2014

  Documentazione online di [!INCLUDE[msCoName](../includes/msconame-md.md)]® per [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]®. Nella documentazione online sono disponibili le descrizioni delle attività e la documentazione di riferimento in cui viene illustrato come eseguire operazioni di gestione dei dati e di Business Intelligence usando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

SQL Server 2016 e versioni successive sono descritte [qui](https://docs.microsoft.com/sql/sql-server/index). SQL Server 2012 e versioni precedenti sono descritte [qui](#previous-versions-gm2014). <!-- ?view= defaults to the latest GA version, to resolve the https '/index' address ambiguity. So '2014' will always be too old to be the default. -->

 **Per provarlo:**  
 ![Macchina virtuale di Azure piccola](../sql-server/media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) Se si ha un account di Azure,  Fare clic **[qui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** per creare rapidamente una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato. Per ulteriori informazioni su SQL Server 2014 (SP1), vedere [le informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865). 
  
## <a name="sql-server-technologies"></a>Tecnologie di SQL Server  

 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono incluse diverse tecnologie di gestione e analisi dei dati. Fare clic sui collegamenti nella tabella seguente per trovare la funzionalità, l'attività e la documentazione di riferimento attinenti a ogni tecnologia.  
  
|||  
|-|-|  
|![Icona motore di database](media/database-engine.gif "Icona motore di database")|[Motore di database](../database-engine/sql-server-database-engine-overview.md)<br /><br /> Il motore di database è il servizio principale per l'archiviazione, l'elaborazione e la protezione dei dati e assicura un accesso controllato e una rapida elaborazione delle transazioni per soddisfare i requisiti delle applicazioni a più alto utilizzo di dati all'interno dell'organizzazione. Il motore di database offre inoltre un supporto completo per garantire alti livelli di disponibilità.|  
|![Logo DQS per l'argomento della Home page di BOL](media/dqs-logo.jpg "Logo DQS per l'argomento della Home page di BOL")|[Data Quality Services](../data-quality-services/data-quality-services.md)<br /><br /> SQL Server Data Quality Services (DQS) offre una soluzione di pulizia dei dati basata sulle informazioni. DQS consente di compilare una Knowledge Base e di usarla per eseguire correzioni di dati e processi di deduplication sui dati in uso tramite mezzi sia computerizzati sia interattivi. È possibile usare servizi dati di riferimento basati su cloud nonché compilare una soluzione di gestione dati che consenta di integrare DQS con SQL Server Integration Services e Master Data Services.|  
|![Icona Analysis Services](media/analysisserver.gif "Icona Analysis Services")|[Analysis Services](https://docs.microsoft.com/analysis-services/analysis-services-overview)<br /><br /> [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è una piattaforma e un set di strumenti di dati analitici per soluzioni di Business Intelligence personali, per team e aziendali. I server e le utilità di progettazione client supportano soluzioni OLAP tradizionali, nuove soluzioni di modellazione tabulare, nonché analitica e collaborazione in modalità self-service tramite PowerPivot, Excel e un ambiente SharePoint Server. In[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sono incluse anche funzionalità di data mining per individuare le relazioni e i modelli nascosti all'interno di elevati volumi di dati.|  
|![Icona Integration Services](media/dts.gif "Icona Integration Services")|[Integration Services](../integration-services/sql-server-integration-services.md)<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è una piattaforma per la compilazione di soluzioni di integrazione dei dati ad alte prestazioni, con pacchetti che consentono l'elaborazione ETL (estrazione, trasformazione e caricamento) per il data warehousing.|  
|![mds_cm_icon](media/mds-cm-icon.gif "mds_cm_icon")|[Master Data Services](../master-data-services/master-data-services.md)<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] è la soluzione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per la gestione dei dati master. Una soluzione compilata in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] garantisce che l'esecuzione di operazioni di creazione di report e di analisi siano basate su informazioni corrette. Usando [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], si crea un repository centrale per i dati master e si gestisce un record controllabile e a protezione diretta di tali dati man mano che vengono modificati nel tempo.|  
|![Icona di replica](media/replication.gif "Icona di replica")|[Replica](../relational-databases/replication/sql-server-replication.md)<br /><br /> La replica è costituita da un set di tecnologie per la copia e la distribuzione di oggetti di database e dati da un database a un altro e dalla successiva sincronizzazione dei database allo scopo di mantenerne la consistenza. Tramite la funzione di replica è possibile distribuire i dati in diverse posizioni a utenti remoti o mobili tramite reti LAN o WAN, connessioni remote, connessioni wireless e Internet.|  
|![Icona Reporting Services](media/reportingservices.gif "Icona Reporting Services")|[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)<br /><br /> Reporting Services offre funzionalità Web aziendali per la gestione e la creazione di report usando come contenuto una serie di origini dati diverse, la pubblicazione dei report in vari formati e la gestione centralizzata della sicurezza e delle sottoscrizioni.|  
  
## <a name="sql-server-information-on-the-web"></a>Informazioni su SQL Server nel Web:  

 [!INCLUDE[msCoName](../includes/msconame-md.md)] pubblica informazioni aggiuntive su [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in diversi siti Web.  
  
 **Siti SQL Server Web**  
  
-   [SQL Server in Microsoft.com](https://go.microsoft.com/fwlink/?linkid=8504)  
  
-   [Centro risorse di SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-resources)  
  
-   [TechCenter di SQL Server](https://go.microsoft.com/fwlink/?linkid=28107)  
  
-   [Centro SQL Server Developer](https://go.microsoft.com/fwlink/?LinkId=42457)  
  
-   [Centro per sviluppatori Data Platform](https://go.microsoft.com/fwlink/?LinkId=17386)  
  
-   [Centro per sviluppatori XML](https://go.microsoft.com/fwlink/?LinkId=42458)  

## <a name="previous-versions-gm2014"></a>SQL Server 2005, 2008, 2012, 2016 +

[!INCLUDE[previous versions](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Vedere anche  

 [Guida di Gestione configurazione SQL Server](../tools/configuration-manager/sql-server-configuration-manager-help.md)  
  
  
