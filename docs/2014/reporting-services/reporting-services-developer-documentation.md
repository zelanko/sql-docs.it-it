---
title: Guida a Developer&#39;s (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8c555d853fd791bed29a06f561021b138526ea1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63255095"
---
# <a name="developer39s-guide-reporting-services"></a>Guida a Developer&#39;s (Reporting Services)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in sono disponibili diverse interfacce di programmazione che è possibile utilizzare nelle proprie applicazioni. È possibile utilizzare le caratteristiche e le funzionalità esistenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per compilare strumenti di gestione e di creazione di report personalizzati nei siti Web e nelle applicazioni Windows oppure per estendere la piattaforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 L'estensione della piattaforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] include la creazione di nuovi componenti e risorse che è possibile utilizzare per l'accesso ai dati, il recapito dei report e altro ancora. È possibile offrire questi componenti e risorse alle società che utilizzano [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nell'organizzazione.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Integrazione di Reporting Services nelle applicazioni](application-integration/integrating-reporting-services-into-applications.md)  
 Viene fornita una panoramica sull'utilizzo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per l'integrazione dei report nelle applicazioni personalizzate. Viene descritto come utilizzare l'accesso con URL diretto e quando utilizzare il servizio Web per accedere al server di report.  
  
 [Servizio Web ReportServer](report-server-web-service/report-server-web-service.md)  
 Il servizio Web ReportServer consente di accedere alle funzionalità complete del server di report. Il servizio Web utilizza SOAP tramite HTTP e funge da interfaccia di comunicazione tra i programmi client e il server di report. Il servizio Web e i relativi metodi espongono le funzionalità del server di report e consentono di creare strumenti personalizzati per qualsiasi parte del ciclo di vita del report, dalla gestione all'esecuzione.  
  
 [Accesso con URL &#40;SSRS&#41;](url-access-ssrs.md)  
 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta un set completo di richieste basate su URL che è possibile utilizzare come punto di accesso semplice e rapido per la navigazione e la visualizzazione dei report. È possibile utilizzare questa tecnologia insieme al servizio Web ReportServer per integrare una soluzione completa di creazione di report nelle applicazioni aziendali personalizzate. L'accesso con URL è particolarmente utile in caso di integrazione dei report come parte di un portale Web o in caso di visualizzazione dei report da un browser.  
  
 [Estensioni di Reporting Services](extensions/reporting-services-extensions.md)  
 L'architettura modulare di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è progettata per offrire estendibilità. È disponibile un'API in codice gestito che consente di sviluppare, installare e gestire in modo semplice le estensioni usate da numerosi componenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . È possibile creare assembly utilizzando [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e aggiungere nuove [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] funzionalità di rendering, sicurezza, recapito e elaborazione dati per soddisfare le esigenze aziendali in continua evoluzione.  
  
 [Elementi dei report personalizzati](custom-report-items/custom-report-items.md)  
 Viene descritto come creare elementi dei report personalizzati per aggiungere funzionalità a RDL o per estendere le funzionalità dei controlli esistenti.  
  
 [Uso di assembly personalizzati con i report](custom-assemblies/using-custom-assemblies-with-reports.md)  
 Viene descritto come utilizzare assembly personalizzati con i report includendo riferimenti al codice nella definizione del report.  
  
 [Accedere al provider WMI per Reporting Services](tools/access-the-reporting-services-wmi-provider.md)  
 Viene descritto come utilizzare il provider WMI di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per gestire le distribuzioni del server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)   
 [Riferimento tecnico &#40;SSRS&#41;](technical-reference-ssrs.md)   
 [&#40;di sviluppo sicuro Reporting Services&#41;](extensions/secure-development/secure-development-reporting-services.md)  
  
  
