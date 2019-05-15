---
title: Impostazioni relative alle informazioni sul dispositivo MHTML | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 996a7f53b5969c9c1d8c39edcd23b62d45a7ff15
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65502733"
---
# <a name="mhtml-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo MHTML
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering dei report in formato MHTML (archivio Web).  
  
|Impostazione|valore|  
|-------------|-----------|  
|**JavaScript**|Indica se JavaScript è supportato nel report visualizzabile.|  
|**OutlookCompat**|Indica se eseguire il rendering con metadati aggiuntivi che comportano una visualizzazione migliore del report in Outlook, Il valore predefinito è **true**.|  
|**Frammento MHTML**|Indica se viene creato un frammento MHTML al posto di un documento MHTML completo. Un frammento MHTML include il contenuto del report in un elemento TABLE e omette gli elementi HTML e BODY. Il valore predefinito è **false**.|  
|**DataVisualizationFitSizing**|Indica il comportamento di adattamento della visualizzazione dei dati all'interno di una tablix. Sono inclusi grafici, misuratori e mappe.<br /><br /> I valori possibili sono **Approssimato** ed **Esatto**.<br /><br /> Il valore predefinito è **Approssimato**. Se l'impostazione viene rimossa dal file **rsreportserver.config** il comportamento predefinito è **Esatto**.<br /><br /> L'abilitazione del ridimensionamento **Esatto** può avere impatto sulle prestazioni perché l'elaborazione per determinare la dimensione esatta potrebbe impiegare più molto tempo di un adattamento approssimativo.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
