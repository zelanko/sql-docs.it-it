---
title: Esportare un report tramite l'accesso con URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 24cc4fbe1a1cadeeb9c2e94fe0da85fce24db8a6
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571493"
---
# <a name="export-a-report-using-url-access"></a>Esportare un report tramite l'accesso con URL
  Facoltativamente, è possibile definire il formato di rendering di un report con il parametro URL *rs:Format* .  Il rendering dei formati HTML 4.0 e HTM5 (estensione per il rendering) viene eseguito nel browser e per gli altri formati il browser richiede di salvare l'output del report in un file locale.  
  
 Ad esempio per ottenere una copia PDF di un report direttamente da un server di report in modalità nativa:  
  
```  
https://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
 Da un server di report in modalità integrata SharePoint:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
 
::: moniker-end
 
 Ad esempio, il comando URL seguente nel browser esporta un report PPTX da un'istanza denominata del server di report:  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 I valori validi per questo parametro sono basati sulle estensioni per il rendering di report installate nel server di report a cui si sta effettuando l'accesso. Le estensioni comuni sono HTML4.0, MHTML, IMAGE, EXCELOPENXML (xlsx), WORDOPENXML (docx), CSV, PDF, XML e NULL. Se un'estensione per il rendering specificata non è installata nel server di report, il rendering del report non viene eseguito e un errore viene generato e visualizzato nel browser.  
  
 Se non si include il parametro *Format* come parte dell'URL, il server di report rileva il browser ed esegue il rendering del report nel formato HTML appropriato.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](../reporting-services/url-access-parameter-reference.md)  
  
  
