---
title: Impostazioni relative alle informazioni sul dispositivo MHTML | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 196afebcabea54fda1b315b1c2f17c0029842f07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280390"
---
# <a name="mhtml-device-information-settings"></a>Impostazioni relative alle informazioni sul dispositivo MHTML
  Nella tabella seguente sono elencate le impostazioni relative alle informazioni sul dispositivo per il rendering dei report in formato MHTML (archivio Web).  
  
|Impostazione|Value|  
|-------------|-----------|  
|**JavaScript**|Indica se JavaScript è supportato nel report visualizzabile.|  
|**OutlookCompat**|Indica se eseguire il rendering con metadati aggiuntivi che comportano una visualizzazione migliore del report in Outlook, Il valore predefinito è `true`.|  
|**Frammento MHTML**|Indica se viene creato un frammento MHTML al posto di un documento MHTML completo. Un frammento MHTML include il contenuto del report in un elemento TABLE e omette gli elementi HTML e BODY. Il valore predefinito è `false`.|  
|**DataVisualizationFitSizing**|Indica il comportamento di adattamento della visualizzazione dei dati all'interno di una tablix. Sono inclusi grafici, misuratori e mappe.<br /><br /> I valori possibili sono **Approssimato** ed **Esatto**.<br /><br /> Il valore predefinito è **Approssimato**. Se l'impostazione viene rimossa dal file **rsreportserver.config** il comportamento predefinito è **Esatto**.<br /><br /> L'abilitazione del ridimensionamento **Esatto** può avere impatto sulle prestazioni perché l'elaborazione per determinare la dimensione esatta potrebbe impiegare più molto tempo di un adattamento approssimativo.|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizzare i parametri di estensione per il rendering in RSReportServer.config.](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
