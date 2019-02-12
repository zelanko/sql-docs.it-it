---
title: Rettangoli e linee (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0933593220b73b8d57d76645ebea05d733e5661
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043112"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Rettangoli e linee (Generatore report e SSRS)
  È possibile utilizzare rettangoli e linee per creare effetti visivi all'interno di un report. Le proprietà di visualizzazione per questi elementi del report si impostano dalla sezione Bordo della scheda Home mentre per le altre proprietà si utilizza il riquadro Proprietà. A un rettangolo è possibile aggiungere caratteristiche come un colore di sfondo o un'immagine, una descrizione comando o un segnalibro.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RectanglesLinesReportParts"></a> Rettangoli e linee come parti del report  
 È possibile pubblicare rettangoli con gli elementi in essi contenuti separatamente dal report come parti del report. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 Non è possibile pubblicare come parti del report gli elementi del report all'interno del rettangolo. Quando gli utenti aggiungono il rettangolo a un report, ottengono il rettangolo e gli elementi in esso contenuti.  
  

  
##  <a name="RectangleAsContainer"></a> Utilizzo di un rettangolo come contenitore  
 È possibile utilizzare un rettangolo come contenitore per altri elementi. Quando si sposta il rettangolo, vengono spostati anche gli elementi contenuti all'interno del rettangolo. Un elemento all'interno del rettangolo consente di visualizzare il nome del rettangolo nella proprietà **Parent** . Per altre informazioni sull'uso di un rettangolo come contenitore, vedere [Aggiungere un rettangolo o un contenitore &#40;Generatore report e SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md) e [Visualizzare dati identici in una matrice e in un grafico &#40;Generatore report&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Un rettangolo è solo un contenitore di elementi che in esso vengono creati o trascinati. Se si disegna un rettangolo intorno a un elemento esistente nell'area di progettazione, il rettangolo non agirà da contenitore. non sarà elencato nella proprietà Parent dell'elemento.  
  
 Quando si utilizzano rettangoli per contenere elementi del report, occorre tenere in considerazione il modo in cui gli elementi verranno modificati nel loro insieme durante il rendering del report. Gli elementi del report che contengono righe ripetute di dati, ad esempio le tabelle, possono espandersi per adattarsi ai dati restituiti da una query modificando di conseguenza il posizionamento degli altri elementi all'interno del rettangolo. Una tabella sposterà gli elementi verso il basso se sono posizionati al di sotto dell'area dati. Per ancorare un elemento, è possibile posizionarlo all'interno di un rettangolo il cui bordo superiore si trovi più in alto rispetto al bordo inferiore della tabella. Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  

  
##  <a name="ReportBorder"></a> Aggiunta di un bordo al report  
 È possibile aggiungere un bordo a un report aggiungendo bordi alle intestazioni, ai piè di pagina e al corpo del report, senza inserire righe o rettangoli. Per altre informazioni, vedere [Aggiungere un bordo a un report &#40;Generatore report e SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md).  
  

  
##  <a name="HowTo"></a> Procedure  
 [Aggiungere un bordo a un report &#40;Generatore report e SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Aggiungere un rettangolo o un contenitore &#40;Generatore report e SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Aggiungere e modificare una linea &#40;Generatore report e SSRS&#41;](add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere un rettangolo o un contenitore &#40;Generatore report e SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
