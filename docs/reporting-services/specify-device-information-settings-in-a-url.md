---
title: Specificare le impostazioni relative alle informazioni sul dispositivo in un URL | Microsoft Docs
description: Informazioni su come specificare le impostazioni relative alle informazioni sul dispositivo in un URL, in particolar modo con l'elemento XML DeviceInfo.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a2d2ef7937d228cc4feeff2c788c1ae3aa3f0b59
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246628"
---
# <a name="specify-device-information-settings-in-a-url"></a>Specificare le impostazioni relative alle informazioni sul dispositivo in un URL
  Le impostazioni relative alle informazioni sul dispositivo sono parametri passati a un'estensione per il rendering. Se si usano i metodi del servizio Web ReportServer di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per eseguire il rendering di un report, viene passato un elemento XML **DeviceInfo** come parametro di input. Gli elementi figlio dell'elemento **DeviceInfo** sono specifici delle impostazioni relative alle informazioni sul dispositivo di diverse estensioni per il rendering. È possibile includere le impostazioni relative alle informazioni sul dispositivo in un URL usando la stringa di parametri *rc:tag=value* , dove *tag* è il nome dell'elemento delle impostazioni relative alle informazioni sul dispositivo a cui si accede. Per altre informazioni sulle impostazioni relative alle informazioni sul dispositivo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente imposta il formato del report specificato su JPEG usando l'impostazione relativa alle informazioni sul dispositivo *OutputFormat* dell'estensione per il rendering dell'immagine. Le interruzioni di riga sono state aggiunte per migliorare la leggibilità:  
  
```  
https://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](../reporting-services/url-access-parameter-reference.md)  
  
  
