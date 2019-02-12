---
title: Using the IDeliveryReportServerInformation Interface for a Delivery Extension (Uso dell'interfaccia IDeliveryReportServerInformation per un'estensione per il recapito) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d211842a43af771e953fd74a15403ba9321f2860
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028002"
---
# <a name="using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension"></a>Utilizzo dell'interfaccia IDeliveryReportServerInformation per un'estensione per il recapito
  L'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation> espone diverse proprietà che è possibile utilizzare per recuperare informazioni su un server di report. È possibile utilizzare queste informazioni per recapitare notifiche e report. Quando si implementa la classe di estensioni per il recapito, si implementa la proprietà <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A>, come richiesto dall'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>. La proprietà <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension.ReportServerInformation%2A> restituisce un oggetto che implementa l'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>. Da questo oggetto è possibile ottenere un elenco di estensioni per il rendering attualmente supportate dal server di report.  
  
 Quanto segue `for` ciclo può essere usato per archiviare un elenco di estensioni per il rendering attualmente disponibili nel server di report in un **ArrayList** oggetto.  
  
```vb  
Dim renderFormats As New ArrayList()  
Dim e As Microsoft.ReportingServices.Interfaces.Extension  
For Each e In  ReportServerInformation.RenderingExtension  
   If e.Visible Then  
      renderFormats.Add(e.Name)  
   End If  
Next e  
```  
  
```csharp  
ArrayList renderFormats = new ArrayList();  
foreach (Microsoft.ReportingServices.Interfaces.Extension e in ReportServerInformation.RenderingExtension)  
{   
   if (e.Visible)  
   {  
      renderFormats.Add(e.Name);  
   }  
}  
```  
  
 Per altre informazioni sull'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IDeliveryReportServerInformation>, [vedere Uso dell'interfaccia IDeliveryReportServerInformation per un'estensione per il recapito](using-the-ideliveryreportserverinformation-interface-for-a-delivery-extension.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.ReportingServices.Interfaces>   
 [Implementazione di un'estensione per il recapito](implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
