---
title: Impostazioni relative alle informazioni sul dispositivo Word | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 776a825c480568be2640d1309c7c3a48970e2c54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571136"
---
# <a name="word-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo Word
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering nel formato [!INCLUDE[ofprword](../includes/ofprword-md.md)] .  
  
|Impostazione|valore|  
|-------------|-----------|  
|**AutoFit**|**False**. L'impostazione di AutoFit è **false** in tutte le tabelle di Word.<br /><br /> **True**. L'impostazione di AutoFit è **true** in tutte le tabelle di Word.<br /><br /> **Never**. I valori di AutoFit non sono impostati in alcuna tabella di Word e viene applicato il comportamento predefinito di Word.<br /><br /> **Default**. AutoFit è impostata per le tabelle più strette rispetto all'area di disegno fisica (larghezza fisica della pagina esclusi i margini) per la pagina logica.|  
|**ExpandToggles**|Indica se per tutti gli elementi che possono essere attivati o disattivati deve venire eseguito il rendering nello stato completamente espanso. Il valore predefinito è **false**.|  
|**FixedPageWidth**|Indica se la larghezza della pagina scritta nel file DOC aumenta in base alla larghezza della pagina più larga nel corpo del report. Il valore predefinito è **false**.|  
|**OmitHyperlinks**|Indica se l'azione collegamento ipertestuale deve essere omessa in tutti gli elementi in cui è impostata. Il valore predefinito è **false**|  
|**OmitDrillthroughs**|Indica se l'azione drill-through deve essere omessa in tutti gli elementi in cui è impostata. Il valore predefinito è **false**|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
