---
title: 'Esercitazione: Aggiungere un istogramma al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 24c8e48ef26d3db2bc7662a36d40725c84b1bbc7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62648251"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un istogramma al report (Generatore report)
  In un istogramma le serie vengono visualizzate come set di barre verticali raggruppate per categoria. Un istogramma può essere utile per:  
  
-   Mostrare le modifiche apportate in un determinato periodo di tempo.  
  
-   Confrontare il valore relativo di più serie.  
  
-   Visualizzare una media mobile per indicare le tendenze.  
  
 Nell'illustrazione seguente è mostrato l'istogramma che verrà creato con una media mobile.  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
1.  [Creare un grafico da Creazione guidata grafico](#Chart)  
  
2.  [Scegliere il tipo di grafico](#ChartType)  
  
3.  [Formattare e assegnare un'etichetta asse orizzontale](#Horizontal)  
  
4.  [Spostare la legenda](#Legend)  
  
5.  [Titolo del grafico](#ChartTitle)  
  
6.  [Formattare e assegnare un'etichetta dell'asse verticale](#Vertical)  
  
7.  [Aggiungere una media mobile](#Average)  
  
8.  [Aggiungere un titolo al Report](#Title)  
  
9. [Salvare il Report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, scegliere un'origine dati e creare un set di dati. Vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo stimato per completare questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Creare un report grafico da Creazione guidata grafico  
 Dal **introduttiva** nella finestra di dialogo, utilizzare la procedura guidata grafico per creare un set di dati incorporato, scegliere un'origine dati condivisa e creare un istogramma.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-chart-report"></a>Per creare un nuovo report grafico  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** .  
  
    > [!NOTE]  
    >  Se il **Guida introduttiva** non viene visualizzato nella finestra di dialogo, dalle **Generatore Report** pulsante, fare clic su **New**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro a destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati**fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o trovare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2009-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2009-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2009-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2009-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2009-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2009-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2009-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2009-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2009-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2009-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2009-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2009-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2009-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2009-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2009-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2009-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati sui quali verrà basato il grafico.  
  
9. Scegliere **Avanti**.  
  
##  <a name="ChartType"></a> 2. Scegliere il tipo di grafico  
 È possibile scegliere tra diversi tipi di grafico predefiniti.  
  
#### <a name="to-add-a-column-chart"></a>Per aggiungere un istogramma  
  
1.  L'istogramma è il tipo di grafico predefinito nella pagina **Scegliere un tipo di grafico** . Scegliere **Avanti**.  
  
2.  Nella pagina **Disponi campi del grafico** trascinare il campo SalesDate in **Categorie**. Le categorie vengono visualizzate sull'asse orizzontale.  
  
3.  Trascinare il campo Sales in **Valori**. Nella casella **Valori** viene visualizzato Sum(Sales) perché per ogni data viene aggregata la somma dei totali di vendita. I valori vengono visualizzati sull'asse verticale.  
  
4.  Scegliere **Avanti**.  
  
5.  Nel **scegliere uno stile** pagina, nella casella di stili, selezionare uno stile.  
  
     Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo. Quando si seleziona uno stile, nel riquadro di anteprima viene visualizzato un esempio del grafico con lo stile selezionato.  
  
6.  Scegliere **Fine**.  
  
     Il grafico verrà aggiunto all'area di progettazione.  
  
7.  Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. Le dimensioni dell'area di progettazione del report vengono aumentate in base alle dimensioni del grafico.  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Horizontal"></a> 3. Formattare l'asse orizzontale e assegnare un'etichetta  
 Per impostazione predefinita, sull'asse orizzontale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>Per formattare una data sull'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic su asse orizzontale e quindi fare clic su **proprietà asse orizzontale**.  
  
3.  Fare clic su **numero**.  
  
4.  Nelle **categoria**, selezionare **data**.  
  
5.  Nella casella **Tipo** selezionare **31 gennaio 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Nella scheda Home fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 La data viene visualizzata nel formato selezionato. Osservare che sull'asse orizzontale del grafico non viene assegnata un'etichetta a ogni categoria. Per impostazione predefinita, vengono incluse solo le etichette che possono essere posizionate accanto all'asse.  
  
 È possibile personalizzare la visualizzazione delle etichette ruotandole e specificando l'intervallo.  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>Per ruotare le etichette dell'asse e modificare l'intervallo di visualizzazione lungo l'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul titolo dell'asse orizzontale e quindi fare clic su **Mostra titolo asse** per rimuovere il titolo. Poiché sull'asse orizzontale vengono visualizzate le date, il titolo non è necessario.  
  
3.  Fare doppio clic su asse orizzontale e quindi fare clic su **proprietà asse orizzontale**.  
  
4.  Nel **opzioni dell'asse** pagina **intervallo dell'asse e l'intervallo**, digitare **3** per **intervallo**. Il grafico verrà visualizzato a intervalli di tre giorni.  
  
5.  Fare clic su **etichette**.  
  
6.  Nelle **Modifica opzioni adattamento etichetta asse**, selezionare **Disabilita adattamento**.  
  
7.  In **Angolo di rotazione etichetta**selezionare **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Il testo di esempio per l'asse orizzontale ruota di 90 gradi.  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Sul grafico le etichette vengono ruotate e visualizzate ogni tre giorni.  
  
##  <a name="Legend"></a> 4. Spostare la legenda  
 La legenda viene creata automaticamente dai dati di categoria e serie.  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>Per spostare la legenda al di sotto dell'area del grafico di un istogramma  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic la legenda del grafico e quindi fare clic su **proprietà legenda**.  
  
3.  Per la **Layout e posizione**, selezionare una posizione diversa. ad esempio la posizione centrale inferiore.  
  
     Quando la legenda viene posizionata alla fine o all'inizio di un grafico, il relativo layout viene modificato da verticale in orizzontale. È possibile selezionare un altro layout nell'elenco a discesa **Layout** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Facoltativo) Poiché in questa esercitazione si fa riferimento a una sola categoria, la legenda non è necessaria. Per rimuovere la legenda, fare doppio clic la legenda e quindi fare clic su **Elimina legenda**.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="ChartTitle"></a> 5. Spostare il titolo del grafico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>Per modificare il titolo di un grafico al di sopra dell'area del grafico  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Selezionare le parole **titolo del grafico** nella parte superiore del grafico e quindi digitare il testo seguente: **Store totali ordini di vendita**.  
  
3.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Vertical"></a> 6. Formattare l'asse verticale e assegnare un'etichetta  
 Per impostazione predefinita, sull'asse verticale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>Per formattare i numeri come valuta sull'asse verticale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sulle etichette dell'asse verticale lateralmente al grafico per selezionarle.  
  
3.  Sulla barra multifunzione, nel **Home** nella scheda il **numero** raggruppare, fare clic il **valuta** pulsante. Le etichette dell'asse cambiano per mostrare il formato della valuta.  
  
4.  Sulla barra multifunzione, nel **Home** nella scheda il **numero** raggruppare, fare clic il **Diminuisci decimali** pulsante due volte, per visualizzare il numero arrotondato al dollaro più vicino.  
  
5.  Fare doppio clic sull'asse verticale e fare clic su **proprietà asse verticale**.  
  
6.  Fare clic su **numero**. Si noti che **valuta** è già selezionato nella **categoria** casella, e **decimali** è già **0** (zero).  
  
7.  Nel **Mostra valori in** fare clic su **migliaia**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare doppio clic sul titolo dell'asse verticale lateralmente al grafico e fare clic su **proprietà titolo asse**.  
  
10. Sostituire il testo di **testo titolo** campo con il testo seguente: **Totale vendite (in migliaia)**. È anche possibile specificare diverse opzioni relative alla formattazione del titolo.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Average"></a> 7. Aggiungere una media mobile  
  
#### <a name="to-add-a-moving-average"></a>Per aggiungere una media mobile  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Fare doppio clic sui **[SUM (Sales)]** campo che si trova il **valori** area e quindi fare clic su **Aggiungi serie calcolata**.  
  
4.  In **Formula**verificare che sia selezionata l'opzione **Media mobile** .  
  
5.  In **Imposta parametri formula**, per l'opzione **Periodo**selezionare **4**.  
  
6.  Fare clic su **bordo**.  
  
7.  Nelle **spessore linea**, selezionare **3pt**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel grafico viene visualizzata una riga in cui è riportata la media mobile delle vendite totali per data, calcolata in base a un intervallo di quattro date.  
  
##  <a name="Title"></a> 8. Aggiungere un titolo al report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
3.  Tipo di **grafico-vendite**, premere INVIO e quindi digitare **gennaio-dicembre 2009**, in modo che risulti simile al seguente:  
  
     **Grafico a barre - Vendite**  
  
     **Gennaio-dicembre 2009**  
  
4.  Selezionare **grafico-vendite**e fare clic sul **grassetto** pulsante la **Font** sezione la **Home** della barra multifunzione.  
  
5.  Selezionare **gennaio-dicembre 2009**e il **Font** sezione il **Home** scheda, impostare la dimensione del carattere su **10**.  
  
6.  (Facoltativo) Potrebbe essere necessario rendere il **titolo** altezza per contenere le due righe di testo da effettua il pull verso il basso le doppie frecce quando si fa clic al centro del bordo inferiore della casella di testo.  
  
     Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Save"></a> 9. Salvare il report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Dal pulsante Generatore report fare clic su **Salva con nome**.  
  
3.  In **Nome**digitare **Istogramma ordini vendita**.  
  
4.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un istogramma al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
