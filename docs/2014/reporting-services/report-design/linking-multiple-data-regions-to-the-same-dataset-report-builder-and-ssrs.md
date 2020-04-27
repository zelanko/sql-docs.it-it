---
title: Collegamento di più aree dati allo stesso set di dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d282636b58352f0ffad1083077bdab9769bd6fdc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105608"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>Collegamento di più aree dati allo stesso set di dati (Generatore report e SSRS)
  È possibile aggiungere più aree dati a un report per fornire visualizzazioni diverse dei dati dello stesso set di dati del report. Può ad esempio verificarsi l'esigenza di visualizzare i dati sia in una tabella che visivamente in un grafico. A tale scopo, è necessario utilizzare espressioni e ambiti identici per le espressioni di filtro, le espressioni di ordinamento e le espressioni di raggruppamento appropriate.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Per utilizzare un grafico e una tabella o una matrice per visualizzare gli stessi dati, può risultare utile avere un'idea delle analogie tra una tabella e i grafici con forme e tra una matrice e i grafici ad area, a barre e gli istogrammi. Una tabella con un solo gruppo di righe può essere visualizzata facilmente come grafico a torta. Se si aggiungono più gruppi di righe, è possibile scegliere tipi diversi di grafici per visualizzare in modo più efficace i gruppi nidificati. Aggiungendo gruppi di righe nidificati a un grafico a torta si aumenta il numero di sezioni della torta. È necessario valutare se il numero di istanze di gruppo per la combinazione di gruppo padre e gruppo figlio è troppo elevato per essere visualizzato in un solo grafico a torta. Nel caso di più valori di gruppo visualizzati come piccole sezioni in un grafico a torta, è possibile impostare una proprietà in base alla quale tutti i valori al di sotto di una determinata soglia vengano visualizzati come un'unica sezione della torta. Per altre informazioni, vedere [Raccogliere piccole sezioni in un grafico a torta &#40;Generatore report e SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
 Una tabella con più gruppi di righe può essere mostrata come un istogramma con più gruppi di categorie. Per altre informazioni, vedere [Visualizzare dati identici in una matrice e in un grafico &#40;Generatore report&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md). Per un esempio di una tabella e un grafico che presentano visualizzazioni diverse dello stesso set di dati del report, fare riferimento al report Product Line Sales negli esempi di report di AdventureWorks. Poiché sia la tabella che il grafico sono collegati allo stesso set di dati in questo report, quando si fa clic sul pulsante di ordinamento interattivo relativo al nome del dipendente nella tabella Top Employees, anche nel grafico Top Employees viene mostrato automaticamente il nuovo ordinamento. Per altre informazioni sul download di questo e di altri report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283) di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Il modo migliore per visualizzare una matrice con più gruppi di righe e colonne è utilizzare un grafico ad area, a barre o un istogramma che contenga sia i gruppi di categorie che di serie. Utilizzare le stesse espressioni di raggruppamento per i gruppi di colonne della matrice e i gruppi di categorie del grafico e le stesse espressioni di raggruppamento per gruppi di righe della matrice e i gruppi di serie del grafico. È necessario ricordare che il numero di istanze di gruppo influisce sulla leggibilità del grafico. È possibile definire i gruppi in base ai valori di intervallo per ridurre il numero di istanze di gruppo di un report. Per altre informazioni, vedere [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Elenca &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)  
  
  
