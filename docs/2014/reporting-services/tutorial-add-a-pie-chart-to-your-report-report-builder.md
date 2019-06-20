---
title: 'Esercitazione: Aggiungere un grafico a torta al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f004241f078a9fb23acbca392f687a9b7c20ae84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099053"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un grafico a torta al report (Generatore report)
  Nei grafici a torta e in quelli ad anello i dati vengono visualizzati come percentuali rispetto a un valore intero. I grafici a torta vengono utilizzati principalmente per eseguire confronti tra gruppi. I grafici a torta e ad anello, insieme ai grafici a piramide e a imbuto, costituiscono un gruppo di grafici noti come grafici con forme. I grafici con forme non includono assi. Quando un campo numerico viene inserito in un grafico con forme, viene calcolata la percentuale di ogni valore rispetto al totale.  
  
 Se sono presenti troppi punti dati su un grafico a torta, le etichette dei punti dati potrebbero essere difficili da leggere. In questo caso è preferibile utilizzare un grafico a linee. Utilizzare grafici a torta solo dopo avere aggregato i dati in pochi punti dati.  
  
 Nell'illustrazione seguente viene mostrato il grafico a torta che verrà creato.  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
 In questa esercitazione verranno illustrate le procedure per:  
  
1.  [Creare un grafico a torta da Creazione guidata grafico](#Chart)  
  
2.  [Scegliere il tipo di grafico](#ChartType)  
  
3.  [Visualizzare percentuali in ogni sezione](#Percentages)  
  
4.  [Combinare le piccole sezioni in un'unica sezione](#CombineSlices)  
  
5.  [Personalizzare l'effetto di disegno](#DrawingEffect)  
  
6.  [Aggiungere un titolo al Report](#Title)  
  
7.  [Salvare il Report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi per la procedura guidata sono consolidati in due procedure. Per istruzioni dettagliate su come selezionare un server di report, aggiungere un'origine dati e un set di dati. Vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo stimato per completare questa esercitazione: 10 minuti  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Creare un grafico a torta da Creazione guidata grafico  
 Dalla finestra di dialogo Riquadro attività iniziale utilizzare la Creazione guidata grafico per creare un set di dati incorporato, scegliere un'origine dati condivisa e creare un grafico a torta.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-chart-report"></a>Per creare un nuovo report grafico  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo Riquadro attività iniziale.  
  
    > [!NOTE]  
    >  Se la finestra di dialogo riquadro attività iniziale non viene visualizzato, dal pulsante Generatore Report, fare clic su **New**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**e fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati sui quali verrà basato il grafico.  
  
9. Scegliere **Avanti**.  
  
##  <a name="ChartType"></a> 2. Scegliere il tipo di grafico  
 È possibile scegliere tra diversi tipi di grafico predefiniti.  
  
#### <a name="to-add-a-pie-chart"></a>Per aggiungere un grafico a torta  
  
1.  Nel **scegliere un tipo di grafico** pagina, fare clic su **torta**e quindi fare clic su **Avanti**. Viene visualizzata la pagina **Disponi campi del grafico** .  
  
     Nella pagina **Disponi campi del grafico** trascinare il campo Product nel riquadro **Categorie** . Le categorie consentono di definire il numero di sezioni nel grafico a torta. In questo esempio, saranno presenti otto sezioni, una per ogni prodotto.  
  
2.  Trascinare il campo Sales nel riquadro **Valori** . Sales rappresenta l'importo delle vendite per la sottocategoria. Nel riquadro **Valori** viene visualizzato `[Sum(Sales)]` perché nel grafico viene mostrata l'aggregazione per ogni prodotto.  
  
3.  Scegliere **Avanti**.  
  
4.  Nel **scegliere uno stile** pagina, selezionare uno stile nel riquadro stili.  
  
     Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo. Quando si seleziona uno stile, nel riquadro di anteprima viene visualizzato un esempio del grafico con lo stile selezionato.  
  
5.  Scegliere **Fine**.  
  
     Il grafico verrà aggiunto all'area di progettazione.  
  
6.  Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. Le dimensioni dell'area di progettazione del report vengono aumentate in base alle dimensioni del grafico.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report viene visualizzato il grafico a torta con otto sezioni, una per ogni prodotto. Le dimensioni di ogni sezione rappresentano le vendite per quel prodotto. Tre delle sezioni sono piuttosto sottili.  
  
##  <a name="Percentages"></a> 3. Visualizzare percentuali in ogni sezione  
 Su ogni sezione della torta, è possibile visualizzare una percentuale per questa sezione rispetto alla torta intera.  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>Per visualizzare le percentuali in ogni sezione del grafico a torta  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sul grafico a torta e scegliere **Mostra etichette dati**. Le etichette dati vengono visualizzate nel grafico.  
  
3.  Fare doppio clic su un'etichetta e quindi fare clic su **proprietà etichetta serie**.  
  
4.  In dati etichetta casella a discesa selezionare **#PERCENT**.  
  
     Per visualizzare i valori come percentuali, la proprietà UseValueAsLabel deve essere impostata su false. Se viene richiesto di impostare questo valore nella finestra di dialogo **Conferma azione** fare clic su **Sì**.  
  
5.  (Facoltativo) Per specificare il numero di cifre decimali visualizzare nell'etichetta, digitare `#PERCENT{Pn}` in cui *n* è il numero di posizioni decimali da visualizzare. Ad esempio, per non visualizzare posizioni decimali, digitare `#PERCENT{P0}`.  
  
    > [!NOTE]  
    >  L'impostazione di**Formato numeri** nella finestra di dialogo **Proprietà etichetta serie** non produrrà alcun effetto quando si formattano le percentuali. Tale opzione consente solo di formattare le etichette come percentuali, senza tuttavia calcolare la percentuale del grafico a torta rappresentata da ciascuna sezione.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report viene visualizzata la percentuale rispetto all'intero per ogni sezione del grafico a torta.  
  
##  <a name="CombineSlices"></a> 4. Combinare le piccole sezioni in una sezione  
 Tre delle sezioni della torta sono piuttosto sottili. È possibile combinare più sezioni piccole in un'unica sezione più grande che le rappresenta tutte.  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>Per combinare le sezioni del grafico a torta inferiori al 5% in un'unica sezione  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Nel **View** nella scheda il **Mostra/Nascondi** gruppo, selezionare **proprietà**.  
  
3.  Nell'area di progettazione fare clic su una sezione del grafico a torta. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
4.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
5.  Impostare la proprietà **CollectedStyle** su **SingleSlice**.  
  
6.  Verificare che la proprietà **CollectedThreshold** sia impostata su 5.  
  
7.  Verificare che la proprietà **CollectedThresholdUsePercent** sia impostata su **True**.  
  
8.  Sulla barra multifunzione, nella **Home** scheda, fare clic su **eseguire** per visualizzare in anteprima il report.  
  
 Nella legenda, la categoria "Other" ora esiste. La nuova sezione del grafico a torta combina tutte le sezioni inferiori al 5% in una sezione che costituisce il 6% della torta intera.  
  
##  <a name="DrawingEffect"></a> 5. Personalizzare l'effetto di disegno  
 In Creazione guidata grafico, lo stile predefinito per un grafico a torta è Oceano che rappresenta un effetto concavo. Tale effetto può essere modificato dopo aver completato la procedura guidata.  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>Per aggiungere un effetto di disegno al grafico a torta  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Se il riquadro proprietà non è già aperta, scegliere il **View** scheda, seleziona **proprietà**.  
  
3.  Fare doppio clic sul grafico a torta. Le proprietà della serie per il grafico a torta verranno visualizzate nel riquadro Proprietà.  
  
4.  Nel riquadro Proprietà espandere il nodo **CustomAttributes** .  
  
5.  Impostare il **PieDrawingStyle** al **SoftEdge**.  
  
    > [!NOTE]  
    >  Gli effetti di disegno e gli effetti tridimensionali sono opzioni esclusive. Se un grafico è applicati, gli effetti tridimensionali **PieDrawingStyle** non è disponibile nel riquadro delle proprietà.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nell'illustrazione seguente viene mostrato il grafico a torta con l'effetto dei bordi sfumati.  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6. Aggiungere un titolo al report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite di fotocamere e di cineprese**, premere INVIO e quindi digitare **Come percentuale delle vendite totali**. Verrà visualizzato quanto segue:  
  
     **Vendite di fotocamere e di cineprese**  
  
     **Come percentuale delle vendite totali**  
  
3.  Selezionare **vendite di fotocamere e cineprese**e fare clic sul **grassetto** pulsante la **Font** sezione del **Home** della barra multifunzione.  
  
4.  Selezionare **come percentuale del totale vendite**e il **Font** sezione il **Home** scheda, impostare la dimensione del carattere su **10**.  
  
5.  (Facoltativo) Per contenere le due righe del testo potrebbe essere necessario aumentare l'altezza della casella di testo Titolo.  
  
     Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Save"></a> 7. Salvare il report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Dal pulsante Generatore report fare clic su **Salva con nome**.  
  
3.  In **Nome**digitare **Grafico a torta - Vendite**.  
  
4.  Fare clic su **Salva**.  
  
 Il report verrà salvato sul server di report.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un grafico a torta al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
