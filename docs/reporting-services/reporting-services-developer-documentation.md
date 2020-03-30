---
title: Documentazione per gli sviluppatori di Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.date: 03/17/2017
ms.openlocfilehash: e2db4a113ebdb53756200879e3797ccbbeec8a52
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68259609"
---
# <a name="reporting-services-developer-documentation"></a>Documentazione per gli sviluppatori di Reporting Services
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] offre diverse interfacce di programmazione che è possibile usare nelle proprie applicazioni. È possibile utilizzare le caratteristiche e le funzionalità esistenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per compilare strumenti di gestione e di creazione di report personalizzati nei siti Web e nelle applicazioni Windows oppure per estendere la piattaforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 L'estensione della piattaforma [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] include la creazione di nuovi componenti e risorse che è possibile utilizzare per l'accesso ai dati, il recapito dei report e altro ancora. È possibile offrire questi componenti e risorse alle società che utilizzano [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nell'organizzazione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] include esercitazioni ed esempi di programmazione di riferimento. Per altre informazioni, vedere [Esempi di Reporting Services](https://msdn.microsoft.com/library/ms160954\(v=sql.110\).aspx) e [Guida per gli sviluppatori: Esercitazioni (Reporting Services)](https://msdn.microsoft.com/library/aa337423\(v=sql.110\).aspx).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Integrazione di Reporting Services nelle applicazioni](../reporting-services/application-integration/integrating-reporting-services-into-applications.md)  
 Viene fornita una panoramica sull'utilizzo di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per l'integrazione dei report nelle applicazioni personalizzate. Viene descritto come utilizzare l'accesso con URL diretto e quando utilizzare il servizio Web per accedere al server di report.  
  
 [Servizio Web ReportServer per applicazioni ASP.net e tradizionali](../reporting-services/report-server-web-service/report-server-web-service.md)  
 Il servizio Web ReportServer consente di accedere alle funzionalità complete del server di report. Il servizio Web utilizza SOAP tramite HTTP e funge da interfaccia di comunicazione tra i programmi client e il server di report. Il servizio Web e i relativi metodi espongono le funzionalità del server di report e consentono di creare strumenti personalizzati per qualsiasi parte del ciclo di vita del report, dalla gestione all'esecuzione.  
 
 [Sviluppare con le API REST per applicazioni moderne](developer/rest-api.md)</br>
 Le API REST di Reporting Services consentono l'accesso programmatico agli oggetti contenuti nel catalogo di un server di report di Reporting Services. Tramite le API REST è possibile esplorare la gerarchia di cartelle, individuare il contenuto di una cartella o scaricare la definizione di un report. È anche possibile creare, aggiornare ed eliminare oggetti.

 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] supporta un set completo di richieste basate su URL che è possibile utilizzare come punto di accesso semplice e rapido per la navigazione e la visualizzazione dei report. È possibile utilizzare questa tecnologia insieme al servizio Web ReportServer per integrare una soluzione completa di creazione di report nelle applicazioni aziendali personalizzate. L'accesso con URL è particolarmente utile in caso di integrazione dei report come parte di un portale Web o in caso di visualizzazione dei report da un browser.  
  
 [Estensioni di Reporting Services](../reporting-services/extensions/reporting-services-extensions.md)  
 L'architettura modulare di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è progettata per offrire estendibilità. È disponibile un'API in codice gestito che consente di sviluppare, installare e gestire in modo semplice le estensioni usate da numerosi componenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . È possibile creare assembly usando [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e aggiungere nuove funzionalità di rendering, sicurezza, recapito ed elaborazione dati di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per soddisfare le esigenze aziendali in continua evoluzione.  
  
 [Elementi dei report personalizzati](../reporting-services/custom-report-items/custom-report-items.md)  
 Viene descritto come creare elementi dei report personalizzati per aggiungere funzionalità a RDL o per estendere le funzionalità dei controlli esistenti.  
  
 [Uso di assembly personalizzati con i report](../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
 Viene descritto come utilizzare assembly personalizzati con i report includendo riferimenti al codice nella definizione del report.  
  
 [Accedere al provider WMI per Reporting Services](../reporting-services/tools/access-the-reporting-services-wmi-provider.md)  
 Viene descritto come utilizzare il provider WMI di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per gestire le distribuzioni del server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Report Definition Language &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)   
 [Sviluppo sicuro &#40;Reporting Services&#41;](../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
