---
title: Formato del file di output XML
description: In SQL Server l'utilità ssbdiagnose può restituire l'output come file XML. Creare un'applicazione per analizzare o segnalare gli errori o visualizzarli in un editor XML.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 1b039d5441ed39c85a8cf1e9468eddfe165aad1c
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83150503"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>Formato del file di output XML (ssbdiagnose)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

L'utilità **ssbdiagnose** restituisce un file di output in formato XML quando viene eseguita con l'opzione **-XML** . Nel file di output XML vengono elencate informazioni di intestazione e gli errori rilevati nella configurazione o nella conversazione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] analizzata. È possibile scrivere un'applicazione per analizzare o generare un report relativo agli errori elencati nel file. In alternativa, è possibile visualizzare il file XML in un editor XML generico, ad esempio XML Notepad.  
  
 Un file di output di **ssbdiangose** contiene un elemento radice DiagnosticInformation con due tipi di figlio:  
  
-   Un elemento Banner con le informazioni di intestazione.  
  
-   Un elemento Issue per ogni problema segnalato da **ssbdiagnose**.  
  
## <a name="diagnosticinformation-root-element"></a>Elemento radice DiagnosticInformation  
  
-   [Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Elemento Banner  
  
-   [Elemento Banner &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Elemento Issue  
  
-   [Elemento Issue &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
