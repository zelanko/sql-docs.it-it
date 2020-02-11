---
title: Aggiungere un filtro (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10ae54e7-0e8a-4dff-995d-05516c51d076
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 38d400b85e8c6f4523bcd20807310912100e587d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106844"
---
# <a name="add-a-filter-report-builder-and-ssrs"></a>Aggiungere un filtro (Generatore report e SSRS)
  Aggiungere un filtro a un set di dati, un'area dati o un gruppo per includere o escludere valori specifici nei calcoli o nella visualizzazione. In fase di esecuzione, i filtri vengono applicati prima al set di dati, poi all'area dati e infine al gruppo procedendo dall'alto verso il basso per le gerarchie di gruppi. In una tabella, una matrice o un elenco i filtri per gruppi di righe, gruppi di colonne e gruppi adiacenti vengono applicati in modo indipendente. Anche in un grafico i filtri per gruppi di categorie e gruppi di serie vengono applicati in modo indipendente.  
  
 Per aggiungere un filtro è necessario specificare una o più equazioni di filtro. Un'equazione di filtro è costituita da un'espressione che identifica i dati da filtrare, da un operatore e dal valore con il quale eseguire il confronto. I dati filtrati e il valore devono essere dello stesso tipo di dati. L'applicazione di filtri ai valori aggregati di un set di dati o un'area dati non è supportata.  
  
 Per filtrare punti dati in un grafico è possibile impostare un filtro in un gruppo di categorie o in un gruppo di serie. Per impostazione predefinita, il grafico usa la funzione predefinita Sum per aggregare valori che fanno parte dello stesso gruppo in un singolo punto dati nella serie. Se si modifica la funzione di aggregazione di una serie, è necessario modificarla anche nell'espressione di filtro.  
  
 Per altre informazioni sul filtro dei set di dati condivisi e incorporati, vedere [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-filter-on-a-data-region"></a>Per impostare un filtro su un'area dati  
  
1.  Aprire un report in visualizzazione **Progettazione** .  
  
2.  Selezionare l'area dati nell'area di progettazione e quindi fare clic con il pulsante destro del mouse su _\<area dati>_ **Proprietà**. Per un misuratore, selezionare **Proprietà pannello del misuratore**. Viene visualizzata la finestra di dialogo _\<area dati>_ **Proprietà**.  
  
    > [!NOTE]  
    >  In un'area dati Tablix fare clic con il pulsante destro del mouse sulla cella d'angolo oppure sull'handle di una riga o colonna e quindi scegliere **Proprietà Tablix**.  
  
3.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
4.  Fare clic su **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
5.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
6.  Nella casella a discesa selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
7.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
8.  Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-tablix-row-or-column-group"></a>Per impostare un filtro su un gruppo di righe o di colonne Tablix  
  
1.  Aprire un report in visualizzazione **Progettazione** .  
  
2.  Fare clic con il pulsante destro del mouse sulla tabella, sulla matrice o sull'area dati dell'elenco nell'area di progettazione per selezionarla. Nel riquadro di raggruppamento vengono visualizzati i gruppi per l'elemento selezionato.  
  
3.  Nel riquadro Raggruppamento fare clic con il pulsante destro del mouse sul gruppo e quindi scegliere **Modifica gruppo**. Verrà visualizzata la finestra di dialogo **Gruppo Tablix** .  
  
4.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
5.  Fare clic su **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
6.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
7.  Nella casella a discesa selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
8.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
9. Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-category-group"></a>Per impostare un filtro su un gruppo di categorie Grafico  
  
1.  Aprire un report in visualizzazione **Progettazione** .  
  
2.  Nell'area di progettazione fare due volte clic sul grafico per visualizzare le aree di rilascio dei campi dati, serie e categoria.  
  
3.  Fare clic con il pulsante destro del mouse su un campo contenuto nell'area di rilascio del campo categoria e scegliere **Proprietà gruppo categorie**.  
  
4.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
5.  Fare clic su **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
6.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
7.  Nella casella a discesa selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
8.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
9. Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-set-a-filter-on-a-chart-series-group"></a>Per impostare un filtro su un gruppo di serie Grafico  
  
1.  Aprire un report in visualizzazione **Progettazione** .  
  
2.  Nell'area di progettazione fare due volte clic sul grafico per visualizzare le aree di rilascio dei campi dati, serie e categoria.  
  
3.  Fare clic con il pulsante destro del mouse su un campo contenuto nell'area di rilascio del campo serie e scegliere **Proprietà gruppo serie**.  
  
4.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
5.  Fare clic su **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
6.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
7.  Nella casella a discesa selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
8.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
9. Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
