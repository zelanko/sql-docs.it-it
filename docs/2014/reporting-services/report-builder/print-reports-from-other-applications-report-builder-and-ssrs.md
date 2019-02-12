---
title: Stampare i report da altre applicazioni (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a5560581-fd57-4a45-b7ea-43b21a8a7419
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 28dcf8712214e7240eb60ef3caa6b28cda31c38e
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031917"
---
# <a name="print-reports-from-other-applications-report-builder-and-ssrs"></a>Stampare i report da altre applicazioni (Generatore report e SSRS)
  Generatore report include un'opzione di esportazione che consente di visualizzare facilmente un report in altre applicazioni. Il comando `Export` è disponibile nella barra degli strumenti del report visualizzata nella parte superiore di un report aperto in un browser o in un'applicazione Web. L'esportazione di un report consente di visualizzarlo in un'altra applicazione. Se ad esempio si esporta un report in formato Excel, il report viene aperto in [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]. L'esportazione di un report per operazioni di stampa è consigliata solo se l'applicazione dispone di caratteristiche di stampa specifiche che si desidera utilizzare.  
  
 Per esportare un report in un'altra applicazione, è necessario che tale applicazione sia installata nel computer in uso. Per eseguire ad esempio l'esportazione in formato Acrobat (PDF), è necessario avere installato Acrobat Reader nel computer. Se si sceglie di esportare un report in formato TIFF, il report verrà aperto dal server di report in uno strumento di visualizzazione associato al tipo di file TIFF. Lo strumento utilizzato varia in base alla versione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in uso. In genere viene utilizzato Visualizzatore immagini e fax per Windows. La risoluzione predefinita corrisponde a 96 dpi (punti per pollice). È possibile aumentarla fino a 300 dpi o 600 dpi, in base alla risoluzione supportata dalla stampante. Per ulteriori informazioni sull'impostazione della risoluzione, vedere la documentazione di Windows.  
  
 Se si sceglie il formato Archivio Web, noto anche come MHTML, il report viene esportato nel browser predefinito. Se si stampa il report dal browser è possibile che vengano inserite informazioni sul percorso del report in fondo a ogni pagina. Nella maggior parte dei casi, è possibile impostare le opzioni del browser in modo che le informazioni sui percorsi non vengano riportate sulle pagine stampate. Per ulteriori informazioni, vedere la documentazione del browser in uso.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Stampare un report &#40;Generatore report e SSRS&#41;](print-a-report-report-builder-and-ssrs.md)   
 [Stampare i report da un browser con il controllo di stampa &#40;Generatore report e SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Esportazione di report &#40;Report e SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [Esportare un report in un altro tipo di file &#40;Generatore report e SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
