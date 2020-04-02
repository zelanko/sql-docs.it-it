---
title: Introduzione alla gestione delle eccezioni in Reporting Services | Microsoft Docs
description: Informazioni su come gestire le eccezioni generate dal servizio Web ReportServer in modo da poter restituire informazioni utili agli utenti quando si verificano errori.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: edaacc97dae131afbc0a9b9f3651877e4952754d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80215725"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>Introduzione alla gestione delle eccezioni in Reporting Services
  Se l'applicazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] invia al servizio Web ReportServer una richiesta che non può essere elaborata, viene restituita al client un'eccezione SOAP. La gestione delle eccezioni generate dal servizio Web ReportServer costituisce una parte importante dello sviluppo delle applicazioni, in quanto quando si verificano gli errori è possibile restituire agli utenti informazioni utili.  
  
 In questa sezione sono incluse informazioni specifiche sulla gestione delle eccezioni, su come impedire agli utenti di immettere input non valido e su come restituire agli utenti informazioni significative sugli errori. Per informazioni generali sulla gestione delle eccezioni, vedere "Gestione e generazione di eccezioni" nella documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Gestione delle eccezioni in Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/handling-exceptions-in-reporting-services.md)|Viene fornita una panoramica delle eccezioni in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e del ruolo di SOAP nel restituire errori da un servizio Web.|  
|[Procedure consigliate per gestione delle eccezioni in Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/best-practices-for-reporting-services-exception-handling.md)|Vengono forniti consigli sulla gestione delle eccezioni in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|[Classe SoapException di Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)|Descrive la classe **SoapException** in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di applicazioni mediante il servizio Web e .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
