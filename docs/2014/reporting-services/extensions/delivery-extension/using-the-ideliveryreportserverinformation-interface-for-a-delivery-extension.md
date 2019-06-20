---
title: Using the IDeliveryReportServerInformation Interface for a Delivery Extension (Uso dell'interfaccia IDeliveryReportServerInformation per un'estensione per il recapito) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- IDeliveryReportServerInformation interface
- delivery extensions [Reporting Services], retrieving report server information
ms.assetid: adbce647-18f3-470c-8114-42f8bcc95dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a94b6da8536ee0269a448b8a446fc0da3f3f576
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164040"
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
  
  
