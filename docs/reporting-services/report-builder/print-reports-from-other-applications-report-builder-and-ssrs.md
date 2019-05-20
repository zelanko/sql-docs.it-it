---
title: Stampare i report da altre applicazioni (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: a5560581-fd57-4a45-b7ea-43b21a8a7419
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: aecaaf98504f9e6228da16b3379efaffcaaaf5a8
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580683"
---
# <a name="print-reports-from-other-applications-report-builder-and-ssrs"></a>Stampare i report da altre applicazioni (Generatore report e SSRS)
  Generatore report include un'opzione di esportazione che consente di visualizzare facilmente un report in altre applicazioni. Il comando **Export** è disponibile nella barra degli strumenti del report visualizzata nella parte superiore di un report aperto in un browser o in un'applicazione Web. L'esportazione di un report consente di visualizzarlo in un'altra applicazione. Se ad esempio si esporta un report in formato Excel, il report viene aperto in [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]. L'esportazione di un report per operazioni di stampa è consigliata solo se l'applicazione dispone di caratteristiche di stampa specifiche che si desidera utilizzare.  
  
 Per esportare un report in un'altra applicazione, è necessario che tale applicazione sia installata nel computer in uso. Per eseguire ad esempio l'esportazione in formato Acrobat (PDF), è necessario avere installato Acrobat Reader nel computer. Se si sceglie di esportare un report in formato TIFF, il report verrà aperto dal server di report in uno strumento di visualizzazione associato al tipo di file TIFF. Lo strumento utilizzato varia in base alla versione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in uso. In genere viene utilizzato Visualizzatore immagini e fax per Windows. La risoluzione predefinita corrisponde a 96 dpi (punti per pollice). È possibile aumentarla fino a 300 dpi o 600 dpi, in base alla risoluzione supportata dalla stampante. Per ulteriori informazioni sull'impostazione della risoluzione, vedere la documentazione di Windows.  
  
 Se si sceglie il formato Archivio Web, noto anche come MHTML, il report viene esportato nel browser predefinito. Se si stampa il report dal browser è possibile che vengano inserite informazioni sul percorso del report in fondo a ogni pagina. Nella maggior parte dei casi, è possibile impostare le opzioni del browser in modo che le informazioni sui percorsi non vengano riportate sulle pagine stampate. Per ulteriori informazioni, vedere la documentazione del browser in uso.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Stampare un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)   
 [Stampare i report da un browser con il controllo di stampa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Esportare un report in un altro tipo di file &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/b577568b-ecbd-44c3-be88-31dab6fc38a2)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
