---
title: 'Esercitazione: Aggiungere un grafico a torta al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 723e8fe5f657d3b9eda2d6ab73966830a13a3aac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099130"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un istogramma al report (Generatore report)
  In un istogramma le serie vengono visualizzate come set di barre verticali raggruppate per categoria. Un istogramma può essere utile per:  
  
-   Mostrare le modifiche apportate in un determinato periodo di tempo.  
  
-   Confrontare il valore relativo di più serie.  
  
-   Visualizzare una media mobile per indicare le tendenze.  
  
 Nell'illustrazione seguente è mostrato l'istogramma che verrà creato con una media mobile.  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Cosa si apprenderà  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
1.  [Creare un grafico da Creazione guidata grafico](#Chart)  
  
2.  [Scegliere il tipo di grafico](#ChartType)  
  
3.  [Formattare l'asse orizzontale e assegnare un'etichetta](#Horizontal)  
  
4.  [Spostare la legenda](#Legend)  
  
5.  [Spostare il titolo del grafico](#ChartTitle)  
  
6.  [Formattare l'asse verticale e assegnare un'etichetta](#Vertical)  
  
7.  [Aggiungere una media mobile](#Average)  
  
8.  [Aggiungere un titolo al report](#Title)  
  
9. [Salva il report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, come scegliere un'origine dati e come creare un set di dati, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo previsto per il completamento di questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-chart-report-from-the-chart-wizard"></a><a name="Chart"></a>1. creare un report grafico da Creazione guidata grafico  
 Nella finestra di dialogo **Introduzione** utilizzare la creazione guidata grafico per creare un set di dati incorporato, scegliere un'origine dati condivisa e creare un istogramma.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-chart-report"></a>Per creare un nuovo report grafico  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Introduzione** .  
  
    > [!NOTE]  
    >  Se la finestra di dialogo **Introduzione** non viene visualizzata, dal pulsante **Generatore report** fare clic su **nuovo**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella **pagina scegliere un set di dati**fare clic su **Crea un set di dati**, quindi fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
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
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati su cui si baserà il grafico.  
  
9. Fare clic su **Avanti**.  
  
##  <a name="2-choose-the-chart-type"></a><a name="ChartType"></a>2. scegliere il tipo di grafico  
 È possibile scegliere tra diversi tipi di grafico predefiniti.  
  
#### <a name="to-add-a-column-chart"></a>Per aggiungere un istogramma  
  
1.  L'istogramma è il tipo di grafico predefinito nella pagina **Scegliere un tipo di grafico** . Fare clic su **Avanti**.  
  
2.  Nella pagina **Disponi campi del grafico** trascinare il campo SalesDate in **Categorie**. Le categorie vengono visualizzate sull'asse orizzontale.  
  
3.  Trascinare il campo Sales in **Valori**. Nella casella **Valori** viene visualizzato Sum(Sales) perché per ogni data viene aggregata la somma dei totali di vendita. I valori vengono visualizzati sull'asse verticale.  
  
4.  Fare clic su **Avanti**.  
  
5.  Nella casella stili della pagina **scegliere uno stile** selezionare uno stile.  
  
     Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo. Quando si seleziona uno stile, nel riquadro di anteprima viene visualizzato un esempio del grafico con lo stile selezionato.  
  
6.  Fare clic su **Fine**.  
  
     Il grafico verrà aggiunto all'area di progettazione.  
  
7.  Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. Le dimensioni dell'area di progettazione del report vengono aumentate in base alle dimensioni del grafico.  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="3-format-and-label-the-horizontal-axis"></a><a name="Horizontal"></a>3. formattare l'asse orizzontale e assegnare un'etichetta  
 Per impostazione predefinita, sull'asse orizzontale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>Per formattare una data sull'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sull'asse orizzontale, quindi scegliere **Proprietà asse orizzontale**.  
  
3.  Fare clic su **numero**.  
  
4.  In **categoria**selezionare **Data**.  
  
5.  Nella casella **Tipo** selezionare **31 gennaio 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Nella scheda Home fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 La data viene visualizzata nel formato selezionato. Osservare che sull'asse orizzontale del grafico non viene assegnata un'etichetta a ogni categoria. Per impostazione predefinita, vengono incluse solo le etichette che possono essere posizionate accanto all'asse.  
  
 È possibile personalizzare la visualizzazione delle etichette ruotandole e specificando l'intervallo.  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>Per ruotare le etichette dell'asse e modificare l'intervallo di visualizzazione lungo l'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sul titolo dell'asse orizzontale, quindi scegliere **Mostra titolo asse** per rimuovere il titolo. Poiché sull'asse orizzontale vengono visualizzate le date, il titolo non è necessario.  
  
3.  Fare clic con il pulsante destro del mouse sull'asse orizzontale, quindi scegliere **Proprietà asse orizzontale**.  
  
4.  Nella pagina **Opzioni asse** , in intervallo **asse**, digitare **3** per **intervallo**. Il grafico verrà visualizzato a intervalli di tre giorni.  
  
5.  Fare clic su **etichette**.  
  
6.  In **modifica opzioni adattamento etichetta asse**selezionare **Disabilita adattamento automatico**.  
  
7.  In **Angolo di rotazione etichetta**selezionare **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Il testo di esempio per l'asse orizzontale ruota di 90 gradi.  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Sul grafico le etichette vengono ruotate e visualizzate ogni tre giorni.  
  
##  <a name="4-move-the-legend"></a><a name="Legend"></a>4. spostare la legenda  
 La legenda viene creata automaticamente dai dati di categoria e serie.  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>Per spostare la legenda al di sotto dell'area del grafico di un istogramma  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sulla legenda nel grafico, quindi scegliere **Proprietà legenda**.  
  
3.  Per **layout e posizione**selezionare una posizione diversa. ad esempio la posizione centrale inferiore.  
  
     Quando la legenda viene posizionata alla fine o all'inizio di un grafico, il relativo layout viene modificato da verticale in orizzontale. È possibile selezionare un altro layout nell'elenco a discesa **Layout** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Facoltativo) Poiché in questa esercitazione si fa riferimento a una sola categoria, la legenda non è necessaria. Per rimuovere la legenda, fare clic con il pulsante destro del mouse sulla legenda, quindi scegliere **Elimina legenda**.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="5-title-the-chart"></a><a name="ChartTitle"></a>5. titolo del grafico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>Per modificare il titolo di un grafico al di sopra dell'area del grafico  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Selezionare le parole **titolo grafico** nella parte superiore del grafico, quindi digitare il testo seguente: **Archivia totali ordini di vendita**.  
  
3.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="6-format-and-label-the-vertical-axis"></a><a name="Vertical"></a>6. formattare l'asse verticale e assegnare un'etichetta  
 Per impostazione predefinita, sull'asse verticale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>Per formattare i numeri come valuta sull'asse verticale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sulle etichette dell'asse verticale lateralmente al grafico per selezionarle.  
  
3.  Sulla barra multifunzione, nel gruppo **numero** della scheda **Home** fare clic sul pulsante **valuta** . Le etichette dell'asse cambiano per mostrare il formato della valuta.  
  
4.  Sulla barra multifunzione, nel gruppo **numero** della scheda **Home** fare clic due volte sul pulsante **Diminuisci decimali** per visualizzare il numero arrotondato al dollaro più vicino.  
  
5.  Fare clic con il pulsante destro del mouse sull'asse verticale e scegliere **Proprietà asse verticale**.  
  
6.  Fare clic su **numero**. Si noti che la **valuta** è già selezionata nella casella **categoria** e le **posizioni decimali** sono già **0** (zero).  
  
7.  Nella casella **Mostra valori in** fare clic su **migliaia**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare clic con il pulsante destro del mouse sul titolo dell'asse verticale lungo il lato del grafico e scegliere **Proprietà titolo asse**.  
  
10. Sostituire il testo nel campo **testo titolo** con il testo seguente: **totale vendite (in migliaia)**. È anche possibile specificare diverse opzioni relative alla formattazione del titolo.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="7-add-a-moving-average"></a><a name="Average"></a>7. aggiungere una media mobili  
  
#### <a name="to-add-a-moving-average"></a>Per aggiungere una media mobile  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Fare clic con il pulsante destro del mouse sul campo **[Sum (Sales)]** che si trova nell'area **valori** , quindi scegliere **Aggiungi serie calcolata**.  
  
4.  In **Formula**verificare che sia selezionata l'opzione **Media mobile** .  
  
5.  In **Imposta parametri formula**, per l'opzione **Periodo**selezionare **4**.  
  
6.  Fare clic su **bordo**.  
  
7.  In **lunghezza riga**selezionare **3PT**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel grafico viene visualizzata una riga in cui è riportata la media mobile delle vendite totali per data, calcolata in base a un intervallo di quattro date.  
  
##  <a name="8-add-a-report-title"></a><a name="Title"></a>8. aggiungere un titolo al report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
3.  Digitare **grafico vendite**, premere INVIO, quindi digitare **gennaio-dicembre 2009**, in modo che abbia un aspetto simile al seguente:  
  
     **Grafico a barre - Vendite**  
  
     **Gennaio - dicembre 2009**  
  
4.  Selezionare **grafico vendite**, quindi fare clic sul pulsante **grassetto** nella sezione **carattere** della scheda **Home** della barra multifunzione.  
  
5.  Selezionare **gennaio-dicembre 2009**e nella sezione **carattere** della scheda **Home** impostare le dimensioni del carattere su **10**.  
  
6.  Opzionale Potrebbe essere necessario fare in modo che la casella di testo del **titolo** sia più alta per contenere le due righe di testo spostando verso il basso le frecce a due punte quando si fa clic al centro del bordo inferiore.  
  
     Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="9-save-the-report"></a><a name="Save"></a>9. salvare il report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sul pulsante Generatore report , quindi su **Salva con nome**.  
  
3.  In **Nome**digitare **Istogramma ordini vendita**.  
  
4.  Fare clic su **Save**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un istogramma al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazioni &#40;Generatore report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
