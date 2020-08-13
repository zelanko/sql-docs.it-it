---
title: Impostazioni relative alle informazioni sul dispositivo Excel | Microsoft Docs
description: Informazioni dettagliate sulle impostazioni relative alle informazioni sul dispositivo disponibili per il rendering in formato Microsoft Excel.
ms.date: 01/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], Excel rendering
- Excel [Reporting Services], rendering
ms.assetid: bb5f3566-f033-4470-be87-1f52fb7a4ab6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4d84c98923a3cee94f64fed863e621821bd7a39
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245130"
---
# <a name="excel-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo Excel
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering nel formato [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Impostazione|Valore|  
|-------------|-----------|  
|**OmitDocumentMap**|Indica se omettere la mappa documento per i report che la supportano. Il valore predefinito è **false**.|  
|**OmitFormulas**|Indica se omettere le formule dal report visualizzabile. Il valore predefinito è **false**.|  
|**SimplePageHeaders**|Indica se viene eseguito il rendering dell'intestazione di pagina del report nell'intestazione di pagina di Excel. Il valore **false** indica che il rendering dell'intestazione di pagina viene eseguito nella prima riga del foglio di lavoro. Il valore predefinito è **false**.|  
|**DynamicImageDpi**|Risoluzione di immagini dinamiche, ad esempio grafici, misuratori e mappe. Il valore predefinito è **96**. Disponibile in Server di report di Power BI (gennaio 2020) e versioni successive|  

  
## <a name="see-also"></a>Vedere anche  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
