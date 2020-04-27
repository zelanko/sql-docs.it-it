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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099053"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un grafico a torta al report (Generatore report)
  Nei grafici a torta e in quelli ad anello i dati vengono visualizzati come percentuali rispetto a un valore intero. I grafici a torta vengono utilizzati principalmente per eseguire confronti tra gruppi. I grafici a torta e ad anello, insieme ai grafici a piramide e a imbuto, costituiscono un gruppo di grafici noti come grafici con forme. I grafici con forme non includono assi. Quando un campo numerico viene inserito in un grafico con forme, viene calcolata la percentuale di ogni valore rispetto al totale.  
  
 Se sono presenti troppi punti dati su un grafico a torta, le etichette dei punti dati potrebbero essere difficili da leggere. In questo caso è preferibile utilizzare un grafico a linee. Utilizzare grafici a torta solo dopo avere aggregato i dati in pochi punti dati.  
  
 Nell'illustrazione seguente viene mostrato il grafico a torta che verrà creato.  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Cosa si apprenderà  
 In questa esercitazione verranno illustrate le procedure per:  
  
1.  [Creare un grafico a torta da Creazione guidata grafico](#Chart)  
  
2.  [Scegliere il tipo di grafico](#ChartType)  
  
3.  [Visualizzare percentuali in ogni sezione](#Percentages)  
  
4.  [Combinare le piccole sezioni in una sezione](#CombineSlices)  
  
5.  [Personalizzare l'effetto di disegno](#DrawingEffect)  
  
6.  [Aggiungere un titolo al report](#Title)  
  
7.  [Salva il report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi per la procedura guidata sono consolidati in due procedure. Per istruzioni dettagliate su come selezionare un server di report, aggiungere un'origine dati e un set di dati, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Il tempo stimato per il completare l'esercitazione è di 10 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-pie-chart-from-the-chart-wizard"></a><a name="Chart"></a>1. creare un grafico a torta da Creazione guidata grafico  
 Dalla finestra di dialogo Riquadro attività iniziale utilizzare la Creazione guidata grafico per creare un set di dati incorporato, scegliere un'origine dati condivisa e creare un grafico a torta.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-chart-report"></a>Per creare un nuovo report grafico  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo Riquadro attività iniziale.  
  
    > [!NOTE]  
    >  Se la finestra di dialogo Introduzione non viene visualizzata, dal pulsante Generatore report fare clic su **nuovo**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**e fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **modifica come testo**.  
  
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
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati su cui si baserà il grafico.  
  
9. Fare clic su **Avanti**.  
  
##  <a name="2-choose-the-chart-type"></a><a name="ChartType"></a>2. scegliere il tipo di grafico  
 È possibile scegliere tra diversi tipi di grafico predefiniti.  
  
#### <a name="to-add-a-pie-chart"></a>Per aggiungere un grafico a torta  
  
1.  Nella pagina **scegliere un tipo di grafico** fare clic su **torta**, quindi su **Avanti**. Viene visualizzata la pagina **Disponi campi del grafico** .  
  
     Nella pagina **Disponi campi del grafico** trascinare il campo Product nel riquadro **Categorie** . Le categorie consentono di definire il numero di sezioni nel grafico a torta. In questo esempio, saranno presenti otto sezioni, una per ogni prodotto.  
  
2.  Trascinare il campo Sales nel riquadro **Valori** . Sales rappresenta l'importo delle vendite per la sottocategoria. Nel riquadro **Valori** viene visualizzato `[Sum(Sales)]` perché nel grafico viene mostrata l'aggregazione per ogni prodotto.  
  
3.  Fare clic su **Avanti**.  
  
4.  Nel riquadro Stili della pagina **scegliere uno stile** selezionare uno stile.  
  
     Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo. Quando si seleziona uno stile, nel riquadro di anteprima viene visualizzato un esempio del grafico con lo stile selezionato.  
  
5.  Fare clic su **Fine**.  
  
     Il grafico verrà aggiunto all'area di progettazione.  
  
6.  Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. Le dimensioni dell'area di progettazione del report vengono aumentate in base alle dimensioni del grafico.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report viene visualizzato il grafico a torta con otto sezioni, una per ogni prodotto. Le dimensioni di ogni sezione rappresentano le vendite per quel prodotto. Tre delle sezioni sono piuttosto sottili.  
  
##  <a name="3-display-percentages-in-each-slice"></a><a name="Percentages"></a>3. visualizzare le percentuali in ogni sezione  
 Su ogni sezione della torta, è possibile visualizzare una percentuale per questa sezione rispetto alla torta intera.  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>Per visualizzare le percentuali in ogni sezione del grafico a torta  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sul grafico a torta e scegliere **Mostra etichette dati**. Le etichette dati vengono visualizzate nel grafico.  
  
3.  Fare clic con il pulsante destro del mouse su un'etichetta e scegliere **Proprietà etichetta serie**.  
  
4.  In dati etichetta, nella casella di riepilogo a discesa, selezionare **#PERCENT**.  
  
     Per visualizzare i valori come percentuali, la proprietà UseValueAsLabel deve essere impostata su false. Se viene richiesto di impostare questo valore nella finestra di dialogo **Conferma azione** fare clic su **Sì**.  
  
5.  Opzionale Per specificare il numero di cifre decimali visualizzate nell' `#PERCENT{Pn}` etichetta, digitare dove *n* è il numero di posizioni decimali da visualizzare. Ad esempio, per non visualizzare posizioni decimali `#PERCENT{P0}`, digitare.  
  
    > [!NOTE]  
    >  L'impostazione di**Formato numeri** nella finestra di dialogo **Proprietà etichetta serie** non produrrà alcun effetto quando si formattano le percentuali. Tale opzione consente solo di formattare le etichette come percentuali, senza tuttavia calcolare la percentuale del grafico a torta rappresentata da ciascuna sezione.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report viene visualizzata la percentuale rispetto all'intero per ogni sezione del grafico a torta.  
  
##  <a name="4-combine-small-slices-into-one-slice"></a><a name="CombineSlices"></a>4. combinare le piccole sezioni in un'unica sezione  
 Tre delle sezioni della torta sono piuttosto sottili. È possibile combinare più sezioni piccole in un'unica sezione più grande che le rappresenta tutte.  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>Per combinare le sezioni del grafico a torta inferiori al 5% in un'unica sezione  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Nel gruppo Mostra **/Nascondi** della scheda **Visualizza** selezionare **proprietà**.  
  
3.  Nell'area di progettazione fare clic su una sezione del grafico a torta. Le proprietà della serie verranno visualizzate nel riquadro Proprietà.  
  
4.  Nella sezione **Generale** espandere il nodo **CustomAttributes** .  
  
5.  Impostare la proprietà **CollectedStyle** su **SingleSlice**.  
  
6.  Verificare che la proprietà **CollectedThreshold** sia impostata su 5.  
  
7.  Verificare che la proprietà **CollectedThresholdUsePercent** sia impostata su **True**.  
  
8.  Nella scheda **Home** della barra multifunzione fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nella legenda, la categoria "Other" ora esiste. La nuova sezione del grafico a torta combina tutte le sezioni inferiori al 5% in una sezione che costituisce il 6% della torta intera.  
  
##  <a name="5-customize-the-drawing-effect"></a><a name="DrawingEffect"></a>5. personalizzare l'effetto di disegno  
 In Creazione guidata grafico, lo stile predefinito per un grafico a torta è Oceano che rappresenta un effetto concavo. Tale effetto può essere modificato dopo aver completato la procedura guidata.  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>Per aggiungere un effetto di disegno al grafico a torta  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Se il riquadro proprietà non è già aperto, selezionare **Proprietà**nella scheda **Visualizza** .  
  
3.  Fare doppio clic sul grafico a torta. Le proprietà della serie per il grafico a torta verranno visualizzate nel riquadro Proprietà.  
  
4.  Nel riquadro Proprietà espandere il nodo **CustomAttributes** .  
  
5.  Impostare **PieDrawingStyle** su **SoftEdge**.  
  
    > [!NOTE]  
    >  Gli effetti di disegno e gli effetti tridimensionali sono opzioni esclusive. Se a un grafico sono applicati effetti tridimensionali, **PieDrawingStyle** non è disponibile nel riquadro proprietà.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nell'illustrazione seguente viene mostrato il grafico a torta con l'effetto dei bordi sfumati.  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="6-add-a-report-title"></a><a name="Title"></a>6. aggiungere un titolo al report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite di fotocamere e di cineprese**, premere INVIO e quindi digitare **Come percentuale delle vendite totali**. Verrà visualizzato quanto segue:  
  
     **Vendite di fotocamere e di cineprese**  
  
     **Come percentuale delle vendite totali**  
  
3.  Selezionare **vendite di fotocamere e**di cineprese e fare clic sul pulsante **grassetto** nella sezione **carattere** della scheda **Home** della barra multifunzione.  
  
4.  Selezionare **come percentuale delle vendite totali**e nella sezione **carattere** della scheda **Home** impostare le dimensioni del carattere su **10**.  
  
5.  (Facoltativo) Per contenere le due righe del testo potrebbe essere necessario aumentare l'altezza della casella di testo Titolo.  
  
     Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="7-save-the-report"></a><a name="Save"></a>7. salvare il report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sul pulsante Generatore report , quindi su **Salva con nome**.  
  
3.  In **Nome**digitare **Grafico a torta - Vendite**.  
  
4.  Fare clic su **Save**.  
  
 Il report verrà salvato sul server di report.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un grafico a torta al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazioni &#40;Generatore report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
