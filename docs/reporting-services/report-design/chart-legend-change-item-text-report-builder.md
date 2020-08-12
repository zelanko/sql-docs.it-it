---
title: Modificare il testo di un elemento della legenda (Generatore report) | Microsoft Docs
description: Informazioni su come modificare il testo di un elemento della legenda in modo da visualizzare altre informazioni sui singoli punti dati in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7f13d4663cf0d4e27148e77eebc59068e8c36924
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681240"
---
# <a name="chart-legend---change-item-text-report-builder"></a>Legenda del grafico - Modificare il testo degli elementi (Generatore report)
  Quando un campo viene posizionato nell'area Valori del grafico, viene generato automaticamente un elemento della legenda contenente il nome di tale campo. Ogni elemento della legenda è collegato a una singola serie nel grafico, ad eccezione dei grafici con forme in cui la legenda è collegata a singoli punti dati anziché a singole serie.  
  
 Nei grafici con forme è possibile modificare il testo di un elemento della legenda in modo da visualizzare ulteriori informazioni sui singoli punti dati. Per visualizzare i valori dei punti dati come percentuali nella legenda, ad esempio, è possibile usare una parola chiave quale **#PERCENT**. Per applicare formati numerici e di data, è possibile aggiungere codici di formato .NET Framework con determinate parole chiave. Per altre informazioni sulle parole chiave, vedere [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
 ![Grafico ottimizzato](../../reporting-services/report-design/media/sharpchart.png "Grafico ottimizzato")  
  
 Nei grafici senza forme è possibile modificare il testo di un elemento della legenda. Se, ad esempio, il nome della serie è "Serie 1", è possibile modificare il testo per renderlo più descrittivo, ad esempio "Vendite anno 2008".  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>Per modificare il testo visualizzato nella legenda in un grafico con forme  
  
1.  Fare clic con il pulsante destro del mouse su una serie o su un campo contenuto nell'area **Valori** e quindi selezionare **Proprietà serie**.  
  
2.  Fare clic su **Legenda** e digitare una parola chiave nella casella **Testo legenda personalizzato** .  
  
 La tabella seguente include esempi di parole chiave specifiche del grafico da usare per la proprietà **Testo legenda personalizzato** . Per altre informazioni sulle parole chiave, vedere [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
|Parola chiave|Descrizione|Esempio di testo visualizzato nella legenda|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|Visualizza la percentuale del valore totale con una posizione decimale.|85.0%|  
|`#VALY`|Visualizza il valore numerico effettivo del campo dati.|17000|  
|`#VALY{C2}`|Visualizza il valore numerico effettivo del campo dati come valuta con due posizioni decimali.|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|Visualizza la rappresentazione testuale del campo categoria, seguita dalla percentuale visualizzata da ogni categoria nel grafico.|Michael Blythe (85%)|  
  
> [!NOTE]  
>  La parola chiave #AXISLABEL può essere valutata solo in fase di esecuzione quando non è specificato alcun campo nell'area **Gruppi di serie** .  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>Per modificare il testo visualizzato nella legenda in un grafico senza forme  
  
1.  Fare clic con il pulsante destro del mouse su una serie o su un campo contenuto nell'area **Valori** e quindi selezionare **Proprietà serie**.  
  
2.  Fare clic su **Legenda** e digitare un'etichetta di legenda nella casella **Testo legenda personalizzato** . La serie verrà aggiornata con il testo specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione della legenda in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)   
 [Formattazione dei colori delle serie in un grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Nascondere elementi legenda nel grafico &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/chart-legend-hide-items-report-builder.md)  
  
  
