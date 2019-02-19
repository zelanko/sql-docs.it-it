---
title: Collegamento di più aree dati allo stesso set di dati (Generatore report e SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: df5f041fb48fce0eec938e09f1718157631e67bb
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296649"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>Collegamento di più aree dati allo stesso set di dati (Generatore report e SSRS)

È possibile aggiungere più aree dati a un report impaginato di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per fornire visualizzazioni diverse dei dati dello stesso set di dati del report. Può ad esempio verificarsi l'esigenza di visualizzare i dati sia in una tabella che visivamente in un grafico. A tale scopo, è necessario utilizzare espressioni e ambiti identici per le espressioni di filtro, le espressioni di ordinamento e le espressioni di raggruppamento appropriate.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Per utilizzare un grafico e una tabella o una matrice per visualizzare gli stessi dati, può risultare utile avere un'idea delle analogie tra una tabella e i grafici con forme e tra una matrice e i grafici ad area, a barre e gli istogrammi. Una tabella con un solo gruppo di righe può essere visualizzata facilmente come grafico a torta. Se si aggiungono più gruppi di righe, è possibile scegliere tipi diversi di grafici per visualizzare in modo più efficace i gruppi nidificati. Aggiungendo gruppi di righe nidificati a un grafico a torta si aumenta il numero di sezioni della torta. È necessario valutare se il numero di istanze di gruppo per la combinazione di gruppo padre e gruppo figlio è troppo elevato per essere visualizzato in un solo grafico a torta. Nel caso di più valori di gruppo visualizzati come piccole sezioni in un grafico a torta, è possibile impostare una proprietà in base alla quale tutti i valori al di sotto di una determinata soglia vengano visualizzati come un'unica sezione della torta. Per altre informazioni, vedere [Raccogliere piccole sezioni in un grafico a torta](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md).  
  
 Una tabella con più gruppi di righe può essere mostrata come un istogramma con più gruppi di categorie. Per altre informazioni, vedere [Visualizzare dati identici in una matrice e in un grafico](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md). Per un esempio di una tabella e un grafico che presentano visualizzazioni diverse dello stesso set di dati del report, fare riferimento al report Product Line Sales negli esempi di report di AdventureWorks. Poiché sia la tabella che il grafico sono collegati allo stesso set di dati in questo report, quando si fa clic sul pulsante di ordinamento interattivo relativo al nome del dipendente nella tabella Top Employees, anche nel grafico Top Employees viene mostrato automaticamente il nuovo ordinamento. Per altre informazioni sul download di questo e di altri report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
 Il modo migliore per visualizzare una matrice con più gruppi di righe e colonne è utilizzare un grafico ad area, a barre o un istogramma che contenga sia i gruppi di categorie che di serie. Utilizzare le stesse espressioni di raggruppamento per i gruppi di colonne della matrice e i gruppi di categorie del grafico e le stesse espressioni di raggruppamento per gruppi di righe della matrice e i gruppi di serie del grafico. È necessario ricordare che il numero di istanze di gruppo influisce sulla leggibilità del grafico. È possibile definire i gruppi in base ai valori di intervallo per ridurre il numero di istanze di gruppo di un report. Per altre informazioni, vedere [Esempi di espressioni di raggruppamento](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
## <a name="next-steps"></a>Passaggi successivi

[Grafici](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Tabelle, matrici ed elenchi](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
[Aree dati nidificate](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
