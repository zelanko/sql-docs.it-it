---
title: Proprietà di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 61f1f50ea7a49acc616a36a4eaf1d3d5fcdf269a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63260921"
---
# <a name="reporting-services-properties"></a>Proprietà di Reporting Services
  Il server di report definisce un set di proprietà di sistema globali del server di report e un set di proprietà degli elementi associate a un singolo elemento archiviato nel database del server di report. Le proprietà definite dal server di report non possono essere eliminate e in alcuni casi sono di sola lettura. Un'applicazione consente di estendere le proprietà di sistema e degli elementi aggiungendo a queste proprietà ulteriori proprietà definite dall'utente.  
  
 I metodi del servizio Web seguenti consentono di recuperare e di impostare le proprietà di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Metodo|Azione|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|Restituisce i valori di una o più proprietà di un elemento nel database del server di report.|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|Restituisce una o più proprietà di sistema.|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|Imposta una o più proprietà di un elemento nel database del server di report.|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|Imposta una o più proprietà di sistema.|  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Proprietà degli elementi del server di report](reporting-services-properties-report-server-item-properties.md)|Vengono descritte le proprietà specifiche degli elementi in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Proprietà di sistema del server di report](reporting-services-properties-report-server-system-properties.md)|Vengono descritte le proprietà di sistema in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../report-server-web-service.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
