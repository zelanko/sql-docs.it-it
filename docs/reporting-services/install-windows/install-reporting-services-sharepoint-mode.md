---
title: Installare la modalità SharePoint di Reporting Services 2016 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
helpviewer_keywords:
- default configuration [Reporting Services]
- installing Reporting Services, SharePoint integrated mode
- installation options [Reporting Services]
ms.assetid: ac6cba68-2665-4a39-8fa3-cb7d7e6723c0
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1aca33e3978b89ccf5f4423e76f0e2ba7888e6a6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406518"
---
# <a name="install-reporting-services-2016-in-sharepoint-mode"></a>Installare la modalità SharePoint di Reporting Services 2016

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services in SharePoint abilita la creazione e la visualizzazione dei report nelle raccolte documenti, il recapito di report della sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante posta elettronica, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], gli avvisi dati e le funzionalità di gestione report, tutto in un'unica distribuzione basata su [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint. Per altre informazioni sulle funzionalità in modalità SharePoint, vedere la sezione relativa al supporto delle funzionalità e alle differenze di comportamento in base alla modalità server in [Server di report di Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md).

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

Ci sono due componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] principali da installare per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint:  

|Installazione|Descrizione|  
|------------------|-----------------|  
|**Server di report:** il server di report di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato in modalità SharePoint|Il server di report gestisce l'elaborazione di dati e report e del rendering, oltre all'elaborazione delle sottoscrizioni e degli avvisi dati. Il server di report in modalità SharePoint è progettato e installato come un servizio condiviso SharePoint.<br /><br /> **Procedura:** usare i supporti di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per installare il server di report.|  
|**Componente aggiuntivo:** il server di report di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint, **rssharepoint.msi**.|Il componente aggiuntivo installa le pagine dell'interfaccia utente (Interfaccia utente) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e funzionalità in un server Web front-end di SharePoint. Le funzionalità dell'interfaccia utente includono [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], pagine dell'amministrazione in Amministrazione centrale SharePoint, pagine delle funzionalità utilizzate nelle raccolte documenti di SharePoint e pagine di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] avvisi dati.<br /><br /> **Procedura:**  il componente aggiuntivo può essere installato con un download Web o dai supporti di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre, vedere [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
  
## <a name="in-this-section"></a>Contenuto della sezione

 [Combinazioni supportate di SharePoint, server Reporting Services e componente aggiuntivo &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
 [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
 [Installare il primo server di report in modalità SharePoint](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md)  
  
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
 [Aggiungere un ulteriore server di report a una farm &#40;con scalabilità orizzontale SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
 [Aggiungere un ulteriore front-end Web di Reporting Services a una farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 [Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services &#40;SharePoint 2013 e SharePoint 2016&#41;](https://msdn.microsoft.com/38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f)  
  
 [Provisioning di sottoscrizioni e avvisi per le applicazioni di servizio SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
 [Attestazioni per il servizio token Windows &#40;c2WTS&#41; e Reporting Services](../../reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md)  

## <a name="next-steps"></a>Passaggi successivi

 [Architettura e flusso di lavoro degli avvisi dati](../../reporting-services/reporting-services-data-alerts.md#AlertingWF)   
 [Gestione avvisi dati per gli amministratori di avvisi](../../reporting-services/data-alert-manager-for-alerting-administrators.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
