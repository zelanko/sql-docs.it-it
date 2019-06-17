---
title: Aggiungere un grafico a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6b595dc-f775-4a53-8554-74a0bf9335ec
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 257df5742c2f8dec7d48c6d3afb4d6c6373d058c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106886"
---
# <a name="add-a-chart-to-a-report-report-builder-and-ssrs"></a>Aggiungere un grafico a un report (Generatore report e SSRS)
  Se si desidera riepilogare i dati in formato visivo, utilizzare un'area dati del grafico. È importante scegliere un tipo di grafico appropriato per il tipo di dati da visualizzare. Tale scelta influirà sull'interpretazione dei dati visualizzati nel grafico. Per altre informazioni, vedere [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 La soluzione più semplice per aggiungere un'area dati del grafico al report è l'esecuzione della procedura guidata Nuovo grafico. La procedura guidata offre istogrammi, grafici a linee, a torta, a barre e ad area. Per questi ed altri tipi di grafico, è possibile anche aggiungere un grafico manualmente.  
  
 Dopo avere aggiunto un'area dati del grafico all'area di progettazione, è possibile trascinare campi del set di dati del report relativi a dati numerici e non numerici nel riquadro Dati grafico del grafico. Fare clic sul grafico per visualizzare il riquadro Dati grafico con le tre aree: Gruppi di serie, Gruppi di categorie e Valori.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-chart-to-a-report-by-using-the-chart-wizard"></a>Per aggiungere un grafico a un report tramite la Creazione guidata grafico  
  
1.  > [!NOTE]  
    >  La Creazione guidata grafico è disponibile unicamente in Generatore report.  
  
     Nella scheda **Inserisci** fare clic su **Grafico**, quindi su **Creazione guidata grafico**.  
  
2.  Seguire i passaggi della procedura guidata **Nuovo grafico** .  
  
3.  Nella scheda **Home** fare clic su **Esegui** per mostrare il report visualizzabile.  
  
4.  Nella scheda **Esegui** fare clic su **Progettazione** per continuare a utilizzare il report.  
  
### <a name="to-add-a-chart-to-a-report"></a>Per aggiungere un grafico a un report  
  
1.  Creare un report e definire un set di dati. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41;](../report-data/report-datasets-ssrs.md).  
  
2.  Nella scheda **Inserisci** fare clic su **Grafico**, quindi su **Inserisci grafico**.  
  
3.  Fare clic sul punto in cui si desidera posizionare l'angolo superiore sinistro del grafico nell'area di progettazione, quindi trascinare fino al punto in cui si desidera posizionare l'angolo inferiore destro.  
  
     Viene visualizzata la finestra di dialogo **Seleziona tipo di grafico** .  
  
4.  Selezionare il tipo di grafico da aggiungere. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Fare clic nel grafico per visualizzare il riquadro **Dati grafico** .  
  
6.  Aggiungere uno o più campi all'area **Valori** . Queste informazioni verranno tracciate sull'asse dei valori.  
  
7.  Aggiungere un campo di raggruppamento all'area **Gruppi di categorie** . Quando si aggiunge questo campo all'area **Gruppi di categorie** , viene creato automaticamente un campo di raggruppamento. Ogni gruppo rappresenta un punto dati nella serie.  
  
8.  Per riepilogare i dati in base alla categoria, fare clic con il pulsante destro del mouse sul campo dati e scegliere **Proprietà serie**. Nella casella **Categoria** selezionare il campo categoria nell'elenco a discesa. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
9. Nella scheda **Home** fare clic su **Esegui** per mostrare il report visualizzabile.  
  
10. Nella scheda **Esegui** fare clic su **Progettazione** per continuare a utilizzare il report.  
  
 Su grafici con assi, ad esempio grafici a barra e istogrammi, potrebbe non essere possibile visualizzare tutte le etichette sull'asse delle categorie. Per altre informazioni su come modificare le etichette dell'asse, vedere [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Tipi di grafico &#40;Generatore report e SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [Punti dati vuoti e Null nei grafici &#40;Generatore report e SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiunta di un grafico a barre al report (Generatore report)](https://go.microsoft.com/fwlink/?LinkId=198052)   
 [Esercitazione: Aggiunta di un grafico a barre a un report (Progettazione report)](https://go.microsoft.com/fwlink/?LinkId=198042)   
 [Esercitazione: Aggiunta di un grafico a torta al report (Generatore report)](https://go.microsoft.com/fwlink/?LinkId=198051)   
 [Esercitazione: Aggiunta di un grafico a torta a un report (Progettazione report)](https://go.microsoft.com/fwlink/?LinkId=198041)  
  
  
