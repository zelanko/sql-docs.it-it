---
title: Specificare colori coerenti in più grafici con forme (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8595050b478743b7092787acf880425b24c5b1e3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960807"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>Specificare i colori coerenti in più grafici con forme (Generatore report e SSRS)
  Nei grafici diversi dai grafici con forme viene selezionato un nuovo colore dalla tavolozza in base all'indice di serie del grafico. Verrà eseguito il mapping delle prime serie sul grafico al primo colore della tavolozza. Questo comportamento non si verifica nei grafici con forme, nei quali di ogni colore nella tavolozza viene eseguito il mapping a un punto dati nel set di dati. Ad esempio viene eseguito il mapping del punto dati 1 al primo colore nella tavolozza e del punto dati 2 alla seconda tavolozza di colori e così via.  
  
 Un punto dati che non presenta valori non viene visualizzato in un grafico con forme. Ciò significa che il punto dati non viene colorato. Se ad esempio il valore del punto 2 è zero, verrà eseguito il mapping del punto 1 al primo colore della tavolozza e verrà eseguito il mapping del punto 3 al secondo colore della tavolozza. Questo metodo risulta utile nel caso di punti vuoti nel set di dati di un grafico a torta in quanto impedisce che venga utilizzato inutilmente un colore della tavolozza se non è necessario disegnare il punto vuoto.  
  
 Come effetto collaterale, quando in un report vengono visualizzati più grafici a torta, potrebbero essere visualizzati colori diversi per i punti dati con lo stesso raggruppamento di categoria. Per risolvere questo inconveniente, è necessario definire colori singoli su cui viene eseguito il mapping a un gruppo di categorie anziché valori di dati singoli. La modalità di esecuzione di questa operazione varia a seconda che si tratti di grafici sparkline in una tabella o in una matrice o di grafici con forme nel report stesso.  
  
 La legenda è collegata alla serie, pertanto qualsiasi colore si specifica per la serie verrà mostrato automaticamente sulla legenda.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>Per specificare colori coerenti in più grafici con forme di tipo sparkline in una tabella o in una matrice  
  
1.  Fare clic nel grafico per visualizzare il riquadro Dati grafico.  
  
2.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse su una categoria e scegliere **Proprietà gruppo categorie**.  
  
3.  Nella casella **Sincronizza gruppi in** della scheda Generale fare clic sul nome della categoria per la quale si desidera sincronizzare i colori, quindi scegliere **OK**.  
  
### <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>Per specificare colori coerenti in più grafici con forme  
  
1.  Fare clic con il pulsante destro del mouse al di fuori del corpo del report, quindi selezionare **Proprietà report**.  
  
2.  In **Codice**digitare il codice seguente nella casella di testo.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  Sarà necessario sostituire le stringhe "Color1" con colori personalizzati. È possibile utilizzare colori denominati, ad esempio "Rosso" oppure il valore esadecimale a sei cifre che rappresenta il colore, ad esempio "#FFFFFF" che indica il nero. Se sono stati definiti più di tre colori, sarà necessario estendere la matrice di colori in modo che il numero di colori della matrice corrisponda al numero di punti nel grafico con forme. È possibile aggiungere nuovi colori alla matrice specificando un elenco delimitato da virgole di valori stringa che contengono colori denominati o rappresentazioni esadecimali dei colori.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Fare clic con il pulsante destro del mouse sul grafico con forme e scegliere **Proprietà serie**.  
  
5.  In **Riempimento**fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione per la proprietà **Colore** .  
  
6.  Digitare l'espressione seguente, in cui "MyCategoryField" è il campo visualizzato nell'area **Gruppi di categorie** :  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione dei colori delle serie in un grafico &#40;Generatore report e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Aggiungere stili smussato, rilievo e trama a un grafico &#40;Generatore report e SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Definire i colori in un grafico mediante la tavolozza &#40;Generatore report e SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [Aggiungere punti vuoti al grafico &#40;Report e SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [Grafici con forme &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Collegamento di più aree dati allo stesso set di dati &#40;Generatore report e SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
