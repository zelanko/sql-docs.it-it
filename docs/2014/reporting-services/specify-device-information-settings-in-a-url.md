---
title: Specificare le impostazioni relative alle informazioni sul dispositivo in un URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d769e272792bb4032c2ad2f0d5469e33a512656b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012572"
---
# <a name="specify-device-information-settings-in-a-url"></a>Specificare le impostazioni relative alle informazioni sul dispositivo in un URL
  Le impostazioni relative alle informazioni sul dispositivo sono parametri passati a un'estensione per il rendering. Se si utilizzano i metodi del servizio Web ReportServer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per eseguire il rendering di un report, come parametro di input viene passato un elemento `DeviceInfo` XML. Gli elementi figlio dell'elemento `DeviceInfo` sono specifici delle impostazioni relative alle informazioni sul dispositivo di diverse estensioni per il rendering. È possibile includere le impostazioni relative alle informazioni sul dispositivo in un URL usando la stringa di parametri *rc:tag=value* , dove *tag* è il nome dell'elemento delle impostazioni relative alle informazioni sul dispositivo a cui si accede. Per altre informazioni sulle impostazioni relative alle informazioni sul dispositivo in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Esempio  
 L'esempio seguente imposta il formato del report specificato su JPEG usando l'impostazione relativa alle informazioni sul dispositivo *OutputFormat* dell'estensione per il rendering dell'immagine. Le interruzioni di riga sono state aggiunte per migliorare la leggibilità:  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](url-access-parameter-reference.md)  
  
  
