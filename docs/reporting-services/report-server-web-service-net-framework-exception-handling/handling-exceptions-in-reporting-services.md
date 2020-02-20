---
title: Gestione delle eccezioni in Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], exceptions
- .NET Framework [Reporting Services]
- exceptions [Reporting Services], about exception handling
- SoapException object
ms.assetid: 1a443432-2db5-48c5-bc29-433b4688082f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7fbf4c9d89d35f4fbb437a41c691f7f8c6578b9b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63028568"
---
# <a name="handling-exceptions-in-reporting-services"></a>Gestione delle eccezioni in Reporting Services
  Quando una richiesta del client dell'API SOAP di Reporting Services non può essere completata, il server di report restituisce un errore al posto dei risultati previsti della chiamata. Quando non è possibile completare una chiamata, viene restituito un errore per il servizio Web ReportServer come elemento XML **Fault** SOAP. L'elemento descrittivo principale dell'errore è l'elemento **dettaglio**, che include tutte le informazioni sull'errore fornite dal server di report, nonché qualsiasi informazioni sull'errore del servizio Web aggiuntiva. L'informazione principale nell'elemento **dettaglio** è il codice di errore del server di report. In base al messaggio e al codice di errore, è possibile determinare l'azione appropriata da eseguire nelle applicazioni. Per altre informazioni sugli errori SOAP, vedere il sito Web World Wide Web Consortium (W3C) all'indirizzo http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>Errori SOAP e .NET Framework  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], se si verifica un errore in una richiesta del client al servizio Web, il server di report comunica l'errore al codice client che chiama il servizio Web generando un oggetto **SoapException**. **SoapException** esegue il wrapping delle informazioni contenute in un errore SOAP. Viene eseguito il mapping della proprietà **Detail** di **SoapException** all'elemento **dettaglio** nell'errore SOAP. Le applicazioni devono intercettare l'oggetto **SoapException** con un blocco try/catch e utilizzare la proprietà **Detail** di **SoapException** per eseguire l'azione appropriata. Per ulteriori informazioni sulla classe **SoapException** e sulla proprietà **Detail** in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Classe SoapException di Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Per altre informazioni sulla classe **SoapException** vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Detail](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introduzione alla gestione delle eccezioni in Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
