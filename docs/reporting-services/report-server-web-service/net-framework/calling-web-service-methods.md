---
title: Chiamata di metodi del servizio Web | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Web service [Reporting Services], calls
- calling Web service
- Report Server Web service, SOAP
- XML Web service [Reporting Services], calls
- Report Server Web service, calls
- XML Web service [Reporting Services], SOAP
- SOAP [Reporting Services], calls
ms.assetid: f6f0c6e3-8bb5-4c44-9d19-1872edc72746
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65da2d36c53f5f00851b36f47396b7bcbf6a6092
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284613"
---
# <a name="calling-web-service-methods"></a>Chiamata ai metodi del servizio Web
  Quando si usa una classe proxy [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] per chiamare le operazioni del servizio Web, si usano i metodi di tale classe. Questi metodi funzionano come qualsiasi altro metodo di una classe nella libreria di classi [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Tutti i metodi del servizio Web dispongono di accesso pubblico e richiedono di fornire il numero appropriato di argomenti e tipi di argomento. Dopo aver creato un'istanza della classe proxy nel progetto, è possibile chiamare i metodi per eseguire operazioni relative ai report tramite il server di report. Il codice C# seguente illustra l'uso del metodo <xref:ReportService2010.ReportingService2010.ListChildren%2A> della classe proxy <xref:ReportService2010.ReportingService2010>. Il codice viene utilizzato per effettuare una chiamata ricorsiva al servizio Web che restituisce una matrice di oggetti <xref:ReportService2010.CatalogItem> contenente un elenco di tutti gli elementi nel database del server di report:  
  
```vb  
Dim rs As New ReportingService2010()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
Dim items As CatalogItem() = rs.ListChildren("/", True)  
```  
  
```csharp  
ReportingService2010 rs = new ReportingService2010();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
CatalogItem[] items = rs.ListChildren("/", true);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
