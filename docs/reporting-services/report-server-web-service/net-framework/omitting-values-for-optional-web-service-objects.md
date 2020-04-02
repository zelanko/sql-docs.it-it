---
title: Omissione di valori per gli oggetti del servizio Web facoltativi | Microsoft Docs
description: Alcune proprietà dei tipi complessi del servizio Web ReportServer supportano la proprietà Specified, che consente di omettere un valore per alcune proprietà scrivibili.
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], omitted values
- XML Web service [Reporting Services], omitted values
- Report Server Web service, omitted values
- omitting values [Reporting Services]
ms.assetid: ceb68b8b-9214-4745-abc9-f47f33ecd6f7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3a7ea9c535092201eaa2c901ef11975bf1461d52
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79509672"
---
# <a name="omitting-values-for-optional-web-service-objects"></a>Omissione di valori per gli oggetti del servizio Web facoltativi
  Alle proprietà di diversi tipi complessi del servizio Web ReportServer è associata una proprietà nota come proprietà Specified. Il nome della proprietà è costituito dal nome della proprietà originale con l'aggiunta della parola "Specified". La presenza di questa proprietà indica che, a volte, è possibile omettere un valore per la proprietà originale. Si tratta di un risultato diretto della conversione da WSDL (Web Service Description Language) a una classe proxy [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Ad esempio, alla proprietà del servizio Web <xref:ReportService2010.DataSourceDefinition.Enabled%2A> del tipo complesso <xref:ReportService2010.DataSourceDefinition> è associata una proprietà denominata <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. Se si compila un'applicazione e non si vuole impostare un valore per la proprietà <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, non è necessario specificare un valore per <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; verrà usato il valore predefinito **true**. È tuttavia necessario impostare <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> su **false**. Se si specifica un valore per la proprietà <xref:ReportService2010.DataSourceDefinition.Enabled%2A>, è necessario impostare anche <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> su **true**. È il caso delle proprietà scrivibili. Per le proprietà di sola lettura, non è necessaria alcuna azione.  
  
> [!IMPORTANT]  
>  La mancata definizione di una proprietà con la tecnica indicata in precedenza può causare un comportamento imprevedibile del servizio Web.  
  
 I tipi di dati che generalmente richiedono la gestione della proprietà Specified aggiuntiva sono **Boolean**, **DateTime**, e **Enumeration**.  
  
 Per un esempio, vedere il metodo <xref:ReportService2010.ReportingService2010.CreateDataSource%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
