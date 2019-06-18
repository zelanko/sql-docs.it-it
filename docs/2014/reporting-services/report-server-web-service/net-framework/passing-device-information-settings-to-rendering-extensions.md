---
title: Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea50de3955ab152cbd92d5fd50ef8b2281a67eb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62518651"
---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering
  In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]le impostazioni relative alle informazioni sul dispositivo vengono usate per passare i parametri di rendering a un'estensione per il rendering. Le impostazioni nel servizio Web ReportServer vengono passate come elemento XML **DeviceInfo** ed elaborate dal server di report. Poiché le impostazioni delle informazioni sul dispositivo dispongono di valori predefiniti, sono considerate argomenti facoltativi nel processo di rendering. È tuttavia possibile usare le impostazioni delle informazioni sul dispositivo per personalizzare il rendering ed eseguire l'override dei valori predefiniti forniti dal server.  
  
 È possibile specificare le impostazioni delle informazioni sul dispositivo in vari modi. A livello di codice è possibile usare il metodo Render. Se si accede a un report tramite il relativo URL, è possibile specificare le informazioni sul dispositivo come parametri URL. È inoltre possibile modificare le impostazioni sulle informazioni sul dispositivo nei file di configurazione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] per specificare a livello globale i parametri di rendering. Per altre informazioni su come specificare i parametri di rendering a livello globale, vedere [Personalizzare i parametri di estensione per il rendering in RSReportServer.config](../../customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
## <a name="passing-device-information-using-the-render-method"></a>Passaggio di informazioni sul dispositivo tramite il metodo Render  
 Per passare le impostazioni delle informazioni sul dispositivo a un'estensione per il rendering, usare il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A>. Ad esempio, è possibile passare la stringa XML seguente al metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A> per creare un frammento HTML durante il rendering in HTML.  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 Quando viene eseguito il rendering di un report come frammento HTML, il contenuto del report si trova all'interno di un elemento TABLE senza l'utilizzo di un elemento HTML o BODY. È possibile usare il frammento HTML per incorporare il report in un documento HTML esistente. Per altre informazioni sulle impostazioni delle informazioni sul dispositivo per l'output HTML, vedere [HTML Device Information Settings](../../html-device-information-settings.md).  
  
## <a name="passing-device-information-using-url-access"></a>Passaggio delle informazioni sul dispositivo con accesso tramite URL  
 È inoltre possibile passare le impostazioni delle informazioni sul dispositivo con accesso tramite URL. Le impostazioni relative alle informazioni sul dispositivo vengono passate come parametri URL. È possibile passare al server di report la stringa di accesso tramite URL per generare un report visualizzabile senza la barra degli strumenti del visualizzatore HTML.  
  
```  
http://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 Per altre informazioni, vedere [Specificare le impostazioni relative alle informazioni sul dispositivo in un URL](../../specify-device-information-settings-in-a-url.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Impostazioni relative alle informazioni sul dispositivo per le estensioni per il rendering &#40;Reporting Services&#41;](../../device-information-settings-for-rendering-extensions-reporting-services.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.Config](../../customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Creazione di applicazioni mediante il servizio Web e .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
