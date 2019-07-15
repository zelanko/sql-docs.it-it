---
title: Formato di File di Output XML (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4b68b8987aad2967447bab72afbb4e3c5665da93
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733543"
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
  
  
