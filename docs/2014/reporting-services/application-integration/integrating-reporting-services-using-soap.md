---
title: Integrazione di Reporting Services tramite SOAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, application integration
- SOAP [Reporting Services]
- SOAP [Reporting Services], about report integration
- integrating reports [Reporting Services]
- Web service [Reporting Services], application integration
ms.assetid: 6bc17af5-883c-4bfa-87d9-48cd7056d145
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b6fffd65b22900d7c505c4b50ec290b95fe9ab4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126190"
---
# <a name="integrating-reporting-services-using-soap"></a>Integrazione di Reporting Services tramite SOAP
  L'API SOAP di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] offre diversi endpoint del servizio Web per lo sviluppo di soluzioni di creazione di report personalizzate. Gli endpoint rientrano attualmente in due categorie, ovvero gestione ed esecuzione. La funzionalità di gestione viene esposta tramite gli endpoint <xref:ReportService2005>, <xref:ReportService2006> e <xref:ReportService2010>. L'endpoint <xref:ReportService2005> viene utilizzato per la gestione di un server di report configurato in modalità nativa, mentre l'endpoint <xref:ReportService2006> viene utilizzato per la gestione di un server di report configurato per la modalità integrata SharePoint. L'endpoint <xref:ReportService2010> unisce le funzionalità di <xref:ReportService2005> e <xref:ReportService2006> e può gestire gli oggetti in un server di report configurati per la modalità nativa o per la modalità integrata SharePoint.  
  
> [!NOTE]  
>  Gli endpoint <xref:ReportService2005> e <xref:ReportService2006> sono deprecati in [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. L'endpoint <xref:ReportService2010> include le funzionalità di entrambi gli endpoint e contiene caratteristiche di gestione aggiuntive.  
  
 La funzionalità di esecuzione viene esposta tramite l'endpoint <xref:ReportExecution2005> e viene utilizzata quando il server di report è configurato in modalità nativa o in modalità integrata SharePoint. Negli argomenti seguenti viene illustrato come utilizzare questi endpoint per lo sviluppo di soluzioni di creazione di report in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, in SharePoint e nelle applicazioni Web.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Uso dell'API SOAP in un'applicazione Windows](integrating-reporting-services-using-soap-windows-application.md)  
 Viene descritto come utilizzare l'API SOAP per integrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un ambiente Windows.  
  
 [Uso dell'API SOAP in un'applicazione Web](integrating-reporting-services-using-soap-web-application.md)  
 Viene descritto come utilizzare l'API SOAP per integrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un ambiente Web.  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione di Reporting Services nelle applicazioni](../application-integration/integrating-reporting-services-into-applications.md)   
 [Servizio Web ReportServer](../report-server-web-service/report-server-web-service.md)   
 [Creazione di applicazioni mediante il servizio Web e .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
