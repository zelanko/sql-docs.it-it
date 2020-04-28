---
title: Installazione per SQL Server 2014 | Microsoft Docs
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
ms.openlocfilehash: 96afef098b711c65e1bcb46d5f687c95061f2c94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75228406"
---
# <a name="installation-for-sql-server-2014"></a>Installazione per SQL Server 2014
 ## <a name="download-sql-server-2014-express"></a>[Scarica SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Grazie a [Scott Hansel](http://www.hanselman.com/) per la raccolta di tutti i collegamenti al pacchetto di installazione in un'unica posizione.**
  
  L'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un singolo albero delle funzionalità per installare tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Strumenti di gestione  
  
-   Componenti di connettività  
  
 È possibile installare singolarmente ogni componente o selezionare una combinazione dei componenti elencati sopra. Per effettuare la scelta migliore tra le edizioni e i componenti disponibili [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]in, vedere [edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è disponibile nelle edizioni a 32 bit e a 64 bit.
 
 **Prova:**  
  
-   Se si ha un account di Azure,  Fare clic **[qui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** per creare rapidamente una macchina virtuale con SQL Server 2014 Service Pack 1 (SP1) già installato. Per ulteriori informazioni su SQL Server 2014 (SP1), vedere [le informazioni sulla versione di SQL Server 2014 Service Pack 1](https://support.microsoft.com/kb/3058865).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
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
  
 [Installare le funzionalità di business intelligence di SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzionalità che fanno parte della piattaforma di Microsoft Business Intelligence includono [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e diverse applicazioni client usate per la creazione o l'uso di dati analitici. In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene descritto come installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Procedure per l'installazione](../../sql-server/install/installation-how-to-topics.md)  
 Vengono forniti i collegamenti agli argomenti sulle procedure per installare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite l'Installazione guidata, il prompt dei comandi, i file di configurazione e SysPrep.  
  
 [Installare SQL Server funzionalità di business intelligence con SharePoint &#40;PowerPivot e Reporting Services&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 In questa sezione viene illustrato come installare funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente SharePoint. e vengono identificate le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili in una versione ed edizione specifiche di SharePoint Nella sezione sono inoltre incluse procedure di installazione per PowerPivot per SharePoint e per Reporting Services in modalità SharePoint.  
  
 [Installazione degli esempi e dei database di esempio di SQL Server](https://sqlserversamples.codeplex.com/)  
 Viene descritto come installare e configurare gli esempi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i database di esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Novità nell'installazione di SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
