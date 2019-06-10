---
title: Installazione di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 230626368ee6ec7048a0a906c5cbe0c404dbe1c3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794835"
---
# <a name="sql-server-installation"></a>Installazione di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

L'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce un singolo albero delle funzionalità per installare tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   Componenti di connettività  
  
A partire da [!INCLUDE[ss2016](../../includes/sssql15-md.md)], Strumenti di gestione di SQL Server non viene più installato dall'albero delle funzionalità principale. Per informazioni dettagliate, vedere [Scaricare SQL Server Management Studio (SSMS) ](../../ssms/download-sql-server-management-studio-ssms.md)  
  
È possibile installare singolarmente ogni componente o selezionare una combinazione dei componenti elencati sopra. Per adottare la scelta migliore tra le edizioni e i componenti disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere le funzionalità supportate dalla propria versione di SQL Server:

- [Edizioni e funzionalità supportate di [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
- [Edizioni e funzionalità supportate di [!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
- [Funzionalità supportate dalle edizioni di [!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>Contenuto della sezione  
Sia che si utilizzi l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o il prompt dei comandi per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il processo di installazione prevede i passaggi seguenti.  
  
[Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
Viene descritto come preparare il computer per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisiti hardware e software.  
-   Requisiti di Controllo configurazione sistema e problemi di blocco.  
-   Considerazioni relative alla sicurezza.  
  
[Installare SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 Vengono descritte le opzioni di installazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Guida di riferimento all'interfaccia utente del programma di installazione di SQL Server](https://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 Vengono descritte le opzioni di installazione disponibili nell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 Vengono descritte le opzioni per l'aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Disinstallare SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 Vengono descritte le routine per disinstallare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
[Installazione del cluster di failover di SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono descritte le modalità di installazione e configurazione del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Installare le funzionalità di business intelligence di SQL Server](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzionalità che fanno parte della piattaforma di Microsoft Business Intelligence includono [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e diverse applicazioni client usate per la creazione o l'uso di dati analitici. In questa sezione della documentazione relativa al programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene descritto come installare [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="more-information"></a>Ulteriori informazioni
[Installare le funzionalità di Business Intelligence di SQL Server con SharePoint &#40;Power Pivot e Reporting Services&#41;](https://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 In questa sezione viene illustrato come installare funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un ambiente SharePoint. e vengono identificate le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibili in una versione ed edizione specifiche di SharePoint Sono incluse anche le procedure di installazione per [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint e per Reporting Services in modalità SharePoint.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Installare il nuovo database di esempio, [Wide World Importers](../../sample/world-wide-importers/wide-world-importers-documentation.md). 
  
[Altri esempi e database di esempio di SQL Server](https://sqlserversamples.codeplex.com/)  
 Viene descritto come installare e configurare gli esempi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i database di esempio.  
  
Vedere la [pagina relativa al centro aggiornamenti di SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) per collegamenti e informazioni per tutte le versioni supportate di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
[Novità relative all'installazione di SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[Requisiti hardware e software per l'installazione di SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
