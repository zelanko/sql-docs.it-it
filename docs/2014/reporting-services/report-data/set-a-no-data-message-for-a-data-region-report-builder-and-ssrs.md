---
title: Impostare una proprietà NoDataMessage per un'area dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4b194714-46f7-4f0e-9632-7f89d9600762
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f2660582b03a121a81976d6bbc12afc1213877c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107092"
---
# <a name="set-a-no-data-message-for-a-data-region-report-builder-and-ssrs"></a>Impostare una proprietà NoDataMessage per un'area dati (Generatore report e SSRS)
  Per specificare il testo da visualizzare nel report visualizzabile al posto di un'area dati senza dati, impostare la proprietà NoRowsMessage di un'area dati tabella, matrice o elenco, la proprietà NoDataMessage di un'area dati del grafico e la proprietà NoDataText per la scala dei colori per una mappa. In fase di esecuzione Elaborazione report esegue la query per ogni set di dati in un report. Tale query non può restituire alcun set di risultati. Per un'area dati associata a un set di dati vuoto, è possibile specificare il testo da visualizzare anziché visualizzare un'area dati vuota. È anche possibile impostare la proprietà NoRowsMessage per un sottoreport quando in nessun set di dati del sottoreport sono presenti dati in fase di esecuzione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-the-norowsmessage-property-for-a-table-matrix-or-list"></a>Per impostare la proprietà NoRowsMessage di una tabella, una matrice o un elenco  
  
1.  Nella visualizzazione Progettazione fare clic sull'area dati tabella, matrice o elenco o sul sottoreport nell'area di progettazione per selezionare l'elemento desiderato. Nel riquadro Proprietà vengono visualizzate le proprietà relative all'elemento selezionato.  
  
2.  Nel riquadro Proprietà digitare il testo che si desidera visualizzare come messaggio nel `NoRowsMessage` campo della proprietà.  
  
     In alternativa, nell'elenco a discesa fare clic su **Espressione** per aprire la finestra di dialogo **Espressione** e creare un'espressione.  
  
### <a name="to-set-the-nodatamessage-property-for-a-chart"></a>Per impostare la proprietà NoDataMessage di un grafico  
  
1.  Nella visualizzazione Progettazione fare clic sul grafico nell'area di progettazione per selezionarlo. Nel riquadro Proprietà vengono visualizzate le proprietà relative all'elemento selezionato.  
  
2.  Nel riquadro Proprietà espandere il nodo per `NoDataMessage`.  
  
3.  In **didascalia**Digitare il testo che si desidera visualizzare come messaggio nel `NoDataMessage` campo della proprietà.  
  
     In alternativa, nell'elenco a discesa fare clic su **Espressione** per aprire la finestra di dialogo **Espressione** e creare un'espressione.  
  
### <a name="to-set-the-norowsmessage-for-a-subreport"></a>Per impostare la proprietà NoRowsMessage di un sottoreport  
  
1.  Nella visualizzazione Progettazione fare clic sul sottoreport nell'area di progettazione per selezionarlo. Nel riquadro Proprietà vengono visualizzate le proprietà relative all'elemento selezionato.  
  
2.  Nel riquadro Proprietà digitare il testo che si desidera visualizzare come messaggio nel `NoRowsMessage` campo della proprietà.  
  
     In alternativa, nell'elenco a discesa fare clic su **Espressione** per aprire la finestra di dialogo **Espressione** e creare un'espressione.  
  
### <a name="to-set-the-nodatatext-property-for-a-color-scale-for-a-map"></a>Per impostare la proprietà NoDataText per una scala dei colori per una mappa  
  
1.  Nella visualizzazione Progettazione fare clic sulla scala dei colori nella mappa per selezionarla. Nel riquadro Proprietà vengono visualizzate le proprietà relative all'elemento selezionato.  
  
2.  Nel riquadro `NoDataText`proprietà digitare il testo che si desidera visualizzare come etichetta per i colori senza valore di dati.  
  
     In alternativa, nell'elenco a discesa fare clic su **Espressione** per aprire la finestra di dialogo **Espressione** e creare un'espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoreport &#40;Generatore report e SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)   
 [Mappe &#40;Generatore report e SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)   
 [Sottoreport &#40;Generatore report e SSRS&#41;](../report-design/subreports-report-builder-and-ssrs.md)  
  
  
