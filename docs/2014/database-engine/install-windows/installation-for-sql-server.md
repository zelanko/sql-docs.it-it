---
title: Installazione di SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5a7e72b429789477a9ae1245be30b18965560ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775362"
---
# <a name="installation-for-sql-server-2014"></a>Installazione per SQL Server 2014
 ## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[Download di SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Grazie per aver preso parte alla [Scott Hanselman](http://www.hanselman.com/) per la raccolta di tutti i collegamenti di pacchetto del programma di installazione in un'unica posizione.**
  
  L'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un singolo albero delle funzionalità per installare tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Strumenti di gestione  
  
-   Componenti di connettività  
  
 È possibile installare singolarmente ogni componente o selezionare una combinazione dei componenti elencati sopra. Per adottare la scelta migliore tra le edizioni e componenti disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è disponibile nelle edizioni a 32 bit e a 64 bit.
 
 **Per provarlo:**  
  
-   Se si ha un account di Azure,  Quindi andare **[qui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** creare rapidamente una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato. Per altre informazioni su SQL Server 2014 (SP1), vedere [informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).  
  
## <a name="in-this-section"></a>In questa sezione  
 Sia che si utilizzi l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il prompt dei comandi per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il processo di installazione prevede i passaggi seguenti.  
  
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
 Viene descritto come preparare il computer per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisiti hardware e software.  
  
-   Requisiti di Controllo configurazione sistema e problemi di blocco.  
  
-   Considerazioni relative alla sicurezza.  
  
 [Installare SQL Server 2014](install-sql-server.md)  
 Vengono descritte le opzioni di installazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Aggiornamento a SQL Server 2014](upgrade-sql-server.md)  
 Vengono descritte le opzioni per l'aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Disinstallare SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)  
 Vengono descritte le routine per disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
 [Installazione del cluster di failover di SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono descritte le modalità di installazione e configurazione del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [Installare le funzionalità di Business Intelligence di SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzionalità che fanno parte della piattaforma di Microsoft Business Intelligence includono [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e diverse applicazioni client usate per la creazione o l'uso di dati analitici. In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene descritto come installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Procedure per l'installazione](../../sql-server/install/installation-how-to-topics.md)  
 Vengono forniti i collegamenti agli argomenti sulle procedure per installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite l'Installazione guidata, il prompt dei comandi, i file di configurazione e SysPrep.  
  
 [Installare le funzionalità SQL Server BI con SharePoint &#40;Reporting Services e PowerPivot&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 In questa sezione viene illustrato come installare funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente SharePoint. e vengono identificate le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili in una versione ed edizione specifiche di SharePoint Nella sezione sono inoltre incluse procedure di installazione per PowerPivot per SharePoint e per Reporting Services in modalità SharePoint.  
  
 [Installazione di SQL Server Samples and Sample Databases](http://sqlserversamples.codeplex.com/)  
 Viene descritto come installare e configurare gli esempi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i database di esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Novità relative all'installazione di SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  
