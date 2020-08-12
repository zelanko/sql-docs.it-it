---
title: Evidenziare i dati del grafico mediante l'aggiunta di strisce (Generatore report) | Microsoft Docs
description: Usare strisce a intervalli orizzontali o verticali per migliorare la leggibilità ed evidenziare le date o un intervallo di chiavi specifico in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b06345fef2d2bc813cfd146c8b31a53b54451859
ms.sourcegitcommit: f898aa83561e94626024916932568ab05e73b656
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/27/2020
ms.locfileid: "84011699"
---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>Evidenziare i dati del grafico mediante l'aggiunta di strisce (Generatore report e SSRS)
  Le strisce o bande sono intervalli orizzontali o verticali che applicano un'ombreggiatura allo sfondo del grafico a intervalli regolari o personalizzati. È possibile utilizzare le strisce per:  
  
-   Migliorare la leggibilità per la ricerca di singoli valori nel grafico. Specificare strisce a intervalli regolari per consentire di separare i punti dati durante la lettura del grafico.  
  
-   Evidenziare date che ricorrono a intervalli regolari. Ad esempio, in un report sulle vendite è possibile utilizzare le strisce per identificare i punti dati relativi ai fine settimana.  
  
-   Evidenziare un intervallo chiave specifico. Nell'ambito dell'esempio precedente, è possibile utilizzare una striscia per evidenziare l'intervallo di vendite più elevato compreso tra 80 e 100 dollari.  
  
 Le strisce non sono applicabili ai tipi di grafico polari o con forme.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>Per visualizzare strisce interlacciate a intervalli regolari in un grafico  
  
1.  Per mostrare strisce orizzontali, fare clic con il pulsante destro del mouse sull'asse del grafico verticale e scegliere **Proprietà asse verticale**.  
  
     Per mostrare strisce verticali, fare clic con il pulsante destro del mouse sull'asse del grafico orizzontale e scegliere **Proprietà asse orizzontale**.  
  
2.  Selezionare l'opzione **Usa interlacciamento** . Sul grafico verranno visualizzate delle strisce di colore grigio.  
  
3.  (Facoltativo) Specificare un colore per le strisce usando l'elenco a discesa **Colore** adiacente.  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>Per visualizzare strisce interlacciate a intervalli personalizzati in un grafico  
  
1.  Per mostrare strisce orizzontali, fare clic con il pulsante destro del mouse sull'asse del grafico verticale e scegliere **Proprietà asse verticale**.  
  
     Per mostrare strisce verticali, fare clic con il pulsante destro del mouse sull'asse del grafico orizzontale e scegliere **Proprietà asse orizzontale**.  
  
     Nella finestra Proprietà verranno visualizzate le proprietà dell'asse.  
  
2.  Nella sezione **Aspetto** del riquadro Proprietà fare clic sul pulsante di modifica della raccolta (...) per la proprietà StripLines per aprire **Editor raccolte ChartStripLine**.  
  
3.  Fare clic su **Aggiungi** per aggiungere una nuova striscia alla raccolta.  
  
4.  Fare clic su StripWidth per specificare la larghezza della striscia, misurata in pollici sul report. Se si vogliono evidenziare date oppure ore, fare clic su StripWidthType e selezionare un intervallo di tempo.  
  
5.  Digitare un valore o un'espressione per l'intervallo in modo da specificare la frequenza con cui si ripeterà la striscia.  Ad esempio, se si specifica un intervallo 10, e la lunghezza riga è 5, le strisce verranno visualizzate in corrispondenza dei valori 0 - 5, 15 - 20, 30 - 35 e così via.  
  
> [!NOTE]  
>  Per impostazione predefinita, l'intervallo è impostato su Automatico. Per questo motivo, non verrà calcolato un intervallo per le strisce personalizzato. Gli intervalli per le strisce verranno calcolati solo se è impostato un valore di intervallo.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Aggiungere una media mobile a un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
