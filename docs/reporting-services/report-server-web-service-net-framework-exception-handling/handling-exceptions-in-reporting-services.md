---
title: Gestione delle eccezioni in Reporting Services | Microsoft Docs
description: Informazioni su come gestire le eccezioni che si verificano in Reporting Services, in modo da poter determinare l'azione successiva appropriata da eseguire nelle applicazioni.
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
ms.openlocfilehash: 2e29de3a0c6b622de2abb411f36a815d7071f16d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216330"
---
# <a name="handling-exceptions-in-reporting-services"></a>Gestione delle eccezioni in Reporting Services
  Quando una richiesta del client dell'API SOAP di Reporting Services non può essere completata, il server di report restituisce un errore al posto dei risultati previsti della chiamata. Quando non è possibile completare una chiamata, viene restituito un errore per il servizio Web ReportServer come elemento XML **Fault** SOAP. L'elemento descrittivo principale dell'errore è l'elemento **dettaglio**, che include tutte le informazioni sull'errore fornite dal server di report, nonché qualsiasi informazioni sull'errore del servizio Web aggiuntiva. L'informazione principale nell'elemento **dettaglio** è il codice di errore del server di report. In base al messaggio e al codice di errore, è possibile determinare l'azione appropriata da eseguire nelle applicazioni. Per altre informazioni sugli errori SOAP, vedere il sito Web World Wide Web Consortium (W3C) all'indirizzo http://www.w3.org/TR/SOAP.  
  
## <a name="soap-faults-and-the-net-framework"></a>Errori SOAP e .NET Framework  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], se si verifica un errore in una richiesta del client al servizio Web, il server di report comunica l'errore al codice client che chiama il servizio Web generando un oggetto **SoapException**. **SoapException** esegue il wrapping delle informazioni contenute in un errore SOAP. Viene eseguito il mapping della proprietà **Detail** di **SoapException** all'elemento **dettaglio** nell'errore SOAP. Le applicazioni devono intercettare l'oggetto **SoapException** con un blocco try/catch e utilizzare la proprietà **Detail** di **SoapException** per eseguire l'azione appropriata. Per ulteriori informazioni sulla classe **SoapException** e sulla proprietà **Detail** in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Classe SoapException di Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md). Per altre informazioni sulla classe **SoapException** vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Detail](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introduzione alla gestione delle eccezioni in Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
