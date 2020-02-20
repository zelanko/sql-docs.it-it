---
title: Impostazioni relative alle informazioni sul dispositivo Excel | Microsoft Docs
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
ms.openlocfilehash: 7a83bcd79a50400888d5a973ad9a743db19b87b5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "76761825"
---
# <a name="excel-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo Excel
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering nel formato [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] .  
  
|Impostazione|valore|  
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
  
  
