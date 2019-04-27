---
title: Formattazione dei punti dati di un grafico (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.serieslabelproperties.general.f1
- "10248"
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c85c464c6ebf32d81c08c319999aa2c6d8b1514c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62654665"
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>Formattazione dei punti dati di un grafico (Generatore report e SSRS)
  Per punto dati si intende l'entità singola più piccola di un grafico. Nei grafici senza forme la rappresentazione dei punti dati dipende dal relativo tipo di grafico. Una serie di linee è ad esempio costituita da uno o più punti dati connessi. Nei grafici con forme i punti dati sono rappresentati dai singoli segmenti o sezioni che costituiscono l'intero grafico. In un grafico a torta, ad esempio, ogni parte è un punto dati. Per altre informazioni, vedere [Tipi di grafico &#40;Generatore report e SSRS&#41;](chart-types-report-builder-and-ssrs.md).  
  
 Uno o più punti dati formano una serie. Per impostazione predefinita, tutte le opzioni di formattazione vengono applicate a tutti i punti dati di una serie. Se si desidera specificare proprietà per i singoli punti dati, è possibile indicare un campo o un'espressione sulla serie che consenta di formattare, in fase di esecuzione, il singolo punto desiderato in base al set di dati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>Aggiunta di descrizioni comandi e di azioni drill-through ai punti dati  
 Per aggiungere descrizioni comandi a ogni punto dati è possibile impostare il valore della proprietà **ToolTip** sulla serie. Le descrizioni comandi consentono agli utenti la visualizzazione di informazioni correlate ai punti dati, quali il nome del gruppo, il valore del punto dati e la percentuale del punto dati rispetto alla serie totale. Per altre informazioni, vedere [Visualizzazione di descrizioni comandi in una serie &#40;Generatore report e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
 È inoltre possibile specificare un'azione drill-through per i punti dati sulla serie in modo da visualizzare un altro report o un URL. È possibile passare parametri per mostrare informazioni relative al punto dati selezionato. Per altre informazioni, vedere [Aggiungere un'azione drill-through a un report &#40;Generatore report e SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>Evidenziazione di singoli punti dati in una serie  
 In qualsiasi grafico senza forme è possibile evidenziare i singoli punti dati specificando un'espressione per la proprietà Color. Per evidenziare ad esempio il valore del punto dati più elevato di una serie, denominato `MyField` , con un colore diverso da quello degli altri punti dati, l'espressione sarà simile alla seguente:  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 Nell'esempio il valore massimo di `MyField` assumerà il colore rosso mentre tutti gli altri punti dati saranno evidenziati in verde. Quando si specifica un colore per la serie usando la relativa proprietà **Fill** , nel grafico vengono sostituiti i colori specificati nella tavolozza. Per altre informazioni, vedere [Formattazione dei colori delle serie in un grafico &#40;Generatore report e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>Posizionamento di etichette dei punti dati in un grafico  
 Per tutti i tipi di grafico è possibile visualizzare etichette dei punti dati facendo clic con il pulsante destro del mouse sul grafico e quindi scegliendo **Mostra etichette dati**. La posizione delle etichette dei punti dati specificata dipende dal tipo di grafico:  
  
-   In un grafico a barre è possibile modificare la posizione dell'etichetta del punto dati usando l'attributo personalizzato **BarLabelStyle** , che può assumere quattro posizioni, ovvero Esterno, A sinistra, Al centro e A destra. Quando lo stile delle etichette del grafico a barre viene impostato su Esterno, le etichette vengono posizionate all'esterno della barra, purché quest'ultima rientri nell'area del grafico. Se l'etichetta non può essere posizionata esternamente alla barra e internamente all'area del grafico, viene inserita nella barra.  
  
-   In un grafico a torta è possibile modificare la posizione dell'etichetta del punto dati usando l'attributo personalizzato **PieLabelStyle** . Quando si posizionano le etichette dei punti dati in un grafico a torta, è necessario tenere presente diversi fattori, quali la dimensione del grafico stesso, lo spazio disponibile tra il grafico e la legenda corrispondente, nonché la dimensione delle etichette. Per altre informazioni, vedere [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md).  
  
-   In un grafico a piramide o a imbuto è possibile modificare la posizione delle etichette dei punti dati usando gli attributi personalizzati **FunnelLabelStyle** e **PyramidLabelStyle** . È possibile impostare questi attributi nel riquadro **Proprietà** dopo aver selezionato un tipo di grafico a piramide o a imbuto.  
  
-   Nei grafici in pila le etichette dei punti dati vengono sempre posizionate all'interno della serie e la proprietà **Position** sull'etichetta della serie viene ignorata.  
  
-   In tutti gli altri tipi di grafico è possibile modificare la posizione dell'etichetta del punto dati usando la proprietà **Position** sull'etichetta della serie. Per impostazione predefinita, nel grafico la posizione delle etichette dei punti dati viene calcolata automaticamente in modo da evitare conflitti tra le etichette. Quando si imposta un valore per la proprietà **Position**, tutte le etichette dei punti dati vengono inserite nella stessa posizione con il rischio che si sovrappongano. Usare questo approccio solo in presenza di un numero ridotto di punti dati.  
  
 Per altre informazioni, vedere [Posizionamento di etichette in un grafico &#40;Generatore report e SSRS&#41;](position-labels-in-a-chart-report-builder-and-ssrs.md).  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>Aggiunta di parole chiave per le etichette dei punti dati, le descrizioni comandi e per il testo legenda  
 Per rappresentare un elemento presente nel grafico è possibile utilizzare parole chiave specifiche con distinzione tra maiuscole e minuscole. Tali parole sono applicabili solo alle descrizioni comandi, al testo personalizzato della legenda e alle proprietà delle etichette dei punti dati. In molti casi una parola chiave del grafico presenta un'espressione semplice equivalente, con la differenza che la parola chiave è più veloce e più facile da digitare. Di seguito viene fornito un elenco delle parole chiave del grafico.  
  
|Parola chiave del grafico|Descrizione|Applicabile al tipo di grafico|Esempio di espressione semplice equivalente|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|Valore Y del punto dati.|All|`=Fields!MyDataField.Value`|  
|#VALY2|Valore Y #2 del punto dati.|Con intervalli, a bolle|None|  
|#VALY3|Valore Y #3 del punto dati.|Azionario, a candela|None|  
|#VALY4|Valore Y #4 del punto dati.|Azionario, a candela|None|  
|#SERIESNAME|Nome della serie.|All|None|  
|#LABEL|Etichetta del punto dati.|All|None|  
|#AXISLABEL|Etichetta del punto dati dell'asse.|Con forme|`=Fields!MyDataField.Value`|  
|#INDEX|Indice del punto dati.|All|None|  
|#PERCENT|Percentuale del valore Y del punto dati.|All|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|Totale di tutti i valori Y della serie|All|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|Testo corrispondente al testo dell'elemento della legenda.|All|None|  
|#AVG|Media di tutti i valori Y della serie|All|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|Minimo di tutti i valori Y della serie|Tutto|`=Min(Fields!MyDataField.Value)`|  
|#MAX|Massimo di tutti i valori Y della serie|All|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|Primo di tutti i valori Y della serie|All|`=First(Fields!MyDataField.Value)`|  
  
 Per formattare la parola chiave, racchiudere tra parentesi una stringa di formato di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Per specificare il valore del punto dati in una descrizione comandi come numero con due posizioni decimali, includere la stringa di formato "N2" tra parentesi, indicando ad esempio il valore "#VALY {N2}" per la proprietà **ToolTip** della serie. Per altre informazioni sulle stringhe di formato di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , vedere [Formattazione dei tipi di dati](https://go.microsoft.com/fwlink/?LinkId=112024) sul sito MSDN. Per altre informazioni sulla formattazione dei numeri in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md).  
  
 Per altre informazioni sull'aggiunta di parole chiave a un grafico, vedere [Visualizzazione di descrizioni comandi in una serie &#40;Generatore report e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md) e [Modificare il testo di un elemento legenda &#40;Generatore report e SSRS&#41;](chart-legend-change-item-text-report-builder.md).  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>Maggiore leggibilità in un grafico con più punti dati  
 Se nel grafico in uso sono presenti più serie, la leggibilità dei punti dati del grafico potrebbe ridursi. Quando si aggiungono più serie al grafico, è consigliabile usare una tecnica che consenta di individuare le procedure ottimali di lettura e interpretazione per ogni serie del grafico. Per altre informazioni, vedere [Più serie in un grafico &#40;Generatore report e SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Per semplicità, quando si usa un grafico con forme, aggiungere un solo campo dati e un solo campo categoria. Per altre informazioni, vedere [Grafici con forme &#40;Generatore report e SSRSS&#41;](charts-report-builder-and-ssrs.md). Se il grafico necessita di più campi dati e di un campo categoria, è possibile modificare il tipo di grafico. È possibile fare clic con il pulsante destro del mouse sulla serie e scegliere **Modifica tipo di grafico**.  
  
## <a name="inserting-data-point-markers"></a>Inserimento di marcatore dei punti dati  
 Un marcatore del punto dati è un indicatore visivo usato per segnalare ogni punto dati di una serie. In un grafico a dispersione il marcatore viene usato per determinare la forma e la dimensione dei singoli punti dati. La dimensione del marcatore specificata dipende dal tipo di grafico. È possibile modificare la dimensione, il colore o lo stile del marcatore. I marcatori non sono disponibili per tipi di grafico con intervalli e forme o per sottotipi di grafico in pila.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Visualizzazione di descrizioni comandi in una serie &#40;Generatore report e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [Visualizzare le etichette dei punti dati al di fuori di un grafico a torta &#40;Generatore report e SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [Visualizzazione di valori percentuale in un grafico a torta &#40;Generatore report e SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRSSSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un grafico a torta al report &#40;Generatore report&#41;](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
