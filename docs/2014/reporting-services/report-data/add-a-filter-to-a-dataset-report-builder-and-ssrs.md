---
title: Aggiungere un filtro a un set di dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3ce57aa0ac17a29b9e8f3b0ea7eef3ad1501a60e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107543"
---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>Aggiungere un filtro a un set di dati (Generatore report e SSRS)
  Aggiungere un filtro a un set di dati per limitare i dati di un report dopo averli recuperati da un'origine dati esterna. Quando si aggiunge un filtro a un set di dati, tutte le parti di report o aree dati utilizzano solo dati che soddisfano le condizioni del filtro.  
  
 Per i set di dati condivisi, un filtro applicato a tutti gli elementi dipendenti deve essere parte della definizione del set di dati condiviso sul server di report. Un report o una parte di report contenente un'istanza di un set di dati condiviso può creare un filtro aggiuntivo che si applica solo all'istanza.  
  
 Per aggiungere un filtro, è necessario specificare una o più condizioni rappresentate da equazioni di filtro. Un'equazione di filtro è costituita da un'espressione che identifica i dati da filtrare, da un operatore e dal valore con il quale eseguire il confronto. I dati filtrati e il valore devono essere dello stesso tipo di dati. L'applicazione di filtri ai valori aggregati di un set di dati non è supportata.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>Per aggiungere un filtro a un set di dati condiviso  
  
1.  Aprire un set di dati condiviso in modalità set di dati condiviso.  
  
2.  Nel gruppo **Set di dati condivisi** della scheda **Home** scegliere Set di dati. Verrà visualizzata la finestra di dialogo **Proprietà set di dati** .  
  
3.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
4.  Scegliere **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
5.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
6.  Nella casella di riepilogo selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
7.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
8.  Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>Per aggiungere un filtro a un set di dati incorporato o a un'istanza del set di dati condiviso  
  
1.  Aprire un report in modalità di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse su un set di dati nel riquadro **Dati report** e scegliere **Proprietà set di dati**. Verrà visualizzata la finestra di dialogo **Proprietà set di dati** .  
  
3.  Fare clic su **Filtri**. Verrà visualizzato l'elenco corrente di equazioni di filtro. Per impostazione predefinita, l'elenco è vuoto.  
  
4.  Scegliere **Aggiungi**. Verrà visualizzata una nuova equazione di filtro vuota.  
  
5.  Nella casella **Espressione**digitare o selezionare l'espressione per il campo da filtrare. Per modificare l'espressione, fare clic sul pulsante dell'espressione (*fx*).  
  
6.  Nella casella a discesa selezionare il tipo di dati corrispondente a quello dell'espressione creata nel passaggio 5.  
  
7.  Nella casella **Operatore** selezionare l'operatore che si desidera utilizzare con il filtro per confrontare i valori nelle caselle **Espressione** e **Valore** . L'operatore scelto determina il numero di valori che verranno utilizzati nel passaggio successivo.  
  
8.  Nella casella **Valore** digitare l'espressione o il valore in base al quale viene valutato il valore nella colonna **Espressione**.  
  
     Per esempi di equazioni di filtro, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere un filtro &#40;Generatore report e SSRS&#41;](../report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  
