---
title: 'Lezione 4: Aggiunta di una tabella al report (Reporting Services) | Microsoft Docs'
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 5ddf2914-bcdd-427d-8cba-0ccb8342f819
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e925dec5eb14365a6c313349599a77ffe1d7ab13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65106012"
---
# <a name="lesson-4-adding-a-table-to-the-report-reporting-services"></a>Lezione 4: Aggiunta di una tabella al report (Reporting Services)

Dopo aver definito il set di dati, è possibile iniziare la progettazione del report. Per creare un layout di report, trascinare gli *oggetti del report* dal riquadro **Casella degli strumenti** all'**area di progettazione**. I tipi di oggetti del report includono ad esempio:

- Tabella
- Casella di testo
- image
- Riga
- Rectangle
- Grafico
- Mappa

Le *aree dati*sono elementi che contengono righe ripetute di dati provenienti dai set di dati sottostanti. Dopo avere aggiunto un'area dati, è possibile aggiungervi dei campi. Un report di base conterrà una sola area dati. È possibile aggiungerne altre per visualizzare altre informazioni, ad esempio un grafico.

## <a name="add-a-table-data-region-and-fields-to-a-report-layout"></a>Aggiungere un'area dati tabella e i campi a un layout di report

1. Selezionare la scheda **Casella degli strumenti** nel riquadro sinistro di Progettazione report. Con il mouse selezionare l'oggetto **Tabella** e trascinarlo nell'area di progettazione del report. In Progettazione report verrà disegnata un'area dati tabella composta da tre colonne al centro dell'area di progettazione. Se la scheda **Casella degli strumenti** non è visualizzata, scegliere **Casella degli strumenti** dal menu **Visualizza**.

    ![ssrs_ssdt_addtable](media/ssrs-ssdt-addtable.png)

    È anche possibile aggiungere una tabella al report dall'area di progettazione. Fare clic con il pulsante destro del mouse sull'area di progettazione e scegliere **Inserisci** > **Tabella**.

2. Nel riquadro **Dati report** espandere AdventureWorksDataset per visualizzare i campi.

3. Trascinare il campo `[Date]` dal riquadro **Dati report** alla prima colonna della tabella.

    > [!IMPORTANT]
    > Quando si rilascia il campo nella prima colonna, si verificano i due eventi indicati di seguito. Per prima cosa, in Progettazione report verrà visualizzato tra parentesi quadre il nome del campo, detto *espressione del campo*, nella cella di dati: `[Date]`. In secondo luogo verrà aggiunta un'etichetta di colonna alla riga di intestazione, proprio sopra l'espressione del campo. Per impostazione predefinita, l'etichetta di colonna è il nome del campo. Se si vuole modificare l'etichetta di colonna, è possibile selezionarla e digitare un nuovo valore.

4. Trascinare il campo `[Order]` dal riquadro **Dati report** alla seconda colonna della tabella.

5. Trascinare il campo `[Product]` dal riquadro **Dati report** alla terza colonna della tabella.

6. Trascinare il campo `[Qty]` sul bordo destro della terza colonna fino a quando non viene visualizzato un cursore verticale e il puntatore del mouse assume l'aspetto del segno più [+]. Quando si rilascia il pulsante del mouse, viene creata una quarta colonna per l'espressione del campo `[Qty]`.

    ![ssrs_tutorial_addcolumn](media/ssrs-tutorial-addcolumn.png)

7. Aggiungere il campo `[LineTotal]` nello stesso modo, creando una quinta colonna. L'etichetta di colonna aggiunta è "Line Total". Progettazione report crea automaticamente un nome descrittivo per la colonna dividendo "LineTotal" in due parole.

Nel diagramma riportato di seguito è illustrata un'area dati della tabella popolata con i campi seguenti: Date, Order, Product, Qty e Line Total.
![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

## <a name="preview-your-report"></a>Visualizzare l'anteprima del report

Mediante la visualizzazione in anteprima di un report è possibile visualizzare il report visualizzabile senza la necessità di pubblicarlo in un server di report. Visualizzare spesso l'anteprima del report durante la progettazione. In questo modo è possibile convalidare la progettazione e le connessioni dati correggendo gli errori e i problemi man mano che si procede.

### <a name="to-preview-a-report"></a>Per visualizzare l'anteprima di un report

- Selezionare la scheda **Anteprima**. Il report verrà eseguito in Progettazione report e verrà mostrato nella visualizzazione **Anteprima**.

    ![ssrs_ssdt_preview](media/ssrs-ssdt-preview.png)

La figura seguente illustra parte del report nella visualizzazione **Anteprima**.

   ![Anteprima, righe di dettaglio della tabella con cinque colonne](media/rs-basictabledetailspreview.png "Anteprima, righe di dettaglio della tabella con cinque colonne")

Esaminare i valori di Date e Line Total. Nella lezione successiva verrà illustrato come formattarli per ottenere una visualizzazione più chiara.

> [!NOTE]
> Scegliere **Salva tutto** dal menu **File** per salvare il report.

## <a name="next-steps"></a>Passaggi successivi

È stata aggiunta un'area dati tabella al report, quindi si sono aggiunti campi all'area dati ed è stata visualizzata l'anteprima del report. Nella lezione successiva verrà illustrato come formattare le intestazioni di colonna e le espressioni dei campi. Passare quindi a [Lezione 5: Formattazione di un report &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md).
  
## <a name="see-also"></a>Vedere anche

[Tabelle &#40;Generatore report e SSRS&#41;](report-design/tables-report-builder-and-ssrs.md)  
[Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
