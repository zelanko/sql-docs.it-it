---
title: Impostazioni relative alle informazioni sul dispositivo PDF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 185b7c9119dbd5a6105152aadcf1241abc6b82ce
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025042"
---
# <a name="pdf-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo PDF
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering dei report nel formato PDF.  
  
|Impostazione|Value|  
|-------------|-----------|  
|**Colonne**|Numero di colonne da impostare per il report. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**ColumnSpacing**|Spaziatura delle colonne da impostare per il report. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**DpiX**|Risoluzione del dispositivo di output nella direzione x.|  
|**DpiY**|Risoluzione del dispositivo di output nella direzione y.|  
|**EndPage**|Ultima pagina del report di cui eseguire il rendering. Il valore predefinito è il valore di `StartPage`.|  
|`HumanReadablePDF`|Indica se il formato PDF deve essere compresso, per migliorare la leggibilità dell'origine. Il valore predefinito è `false.`|  
|**MarginBottom**|Valore in pollici del margine inferiore da impostare per il report. È necessario includere un numero intero o un valore decimale seguito da "in", ad esempio 1in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**MarginLeft**|Valore in pollici del margine sinistro da impostare per il report. È necessario includere un numero intero o un valore decimale seguito da "in", ad esempio 1in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**MarginRight**|Valore in pollici del margine destro da impostare per il report. È necessario includere un numero intero o un valore decimale seguito da "in", ad esempio 1in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**MarginTop**|Valore in pollici del margine superiore da impostare per il report. È necessario includere un numero intero o un valore decimale seguito da "in", ad esempio 1in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**PageHeight**|Altezza di pagina in pollici da impostare per il report. È necessario includere un numero intero o un valore decimale seguito da "in", ad esempio 11in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|**PageWidth**|Larghezza di pagina in pollici da impostare per il report. È necessario includere un valore intero o decimale seguito da "in", ad esempio 8.5in. Questo valore ha la priorità sulle impostazioni originali del report.|  
|`StartPage`|Prima pagina del report di cui eseguire il rendering. Il valore `0` indica che viene eseguito il rendering di tutte le pagine. Il valore predefinito è `1`.|  
  
## <a name="see-also"></a>Vedere anche  
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
