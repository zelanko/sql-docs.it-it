---
title: 'Esercitazione: Aggiungere un grafico a torta al report (Generatore report) | Microsoft Docs'
description: Informazioni su come creare un report impaginato di Reporting Services con un istogramma che visualizza una serie come set di barre verticali raggruppate per categoria.
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 450e625fba58eaa6ff1d9e9fe13065bf934a633b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245688"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un istogramma al report (Generatore report)
In questa esercitazione si creerà un report impaginato di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] con un istogramma che visualizza una serie come set di barre verticali raggruppate per categoria. 

Gli istogrammi sono utili per:  
  
-   Mostrare le modifiche apportate in un determinato periodo di tempo.  
-   Confrontare il valore relativo di più serie.  
-   Visualizzare una media mobile per indicare le tendenze.  
  
Nell'illustrazione seguente è mostrato l'istogramma che verrà creato con una media mobile.  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, come scegliere un'origine dati e come creare un set di dati, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo stimato per il completamento dell'esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-chart-report-from-the-chart-wizard"></a><a name="Chart"></a>1. Creare un report grafico da Creazione guidata grafico  
In questa sezione si usa Creazione guidata grafico per creare un set di dati incorporato, scegliere un'origine dati condivisa e creare un istogramma.  
  
> [!NOTE]  
> La query di questa esercitazione contiene i valori dei dati, pertanto non è necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
### <a name="to-create-a-chart-report"></a>Per creare un report grafico  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal computer, dal portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o in modalità integrata SharePoint.  
  
    Si apre la finestra di dialogo **Nuovo report o set di dati** .  
  
    Se la finestra di dialogo **Nuovo report o set di dati** non viene visualizzata, scegliere **Nuovo** dal menu **File**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati**fare clic su **Crea un set di dati**, quindi scegliere **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    > L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui ( **!** ) per visualizzare i dati su cui si baserà il grafico.  
  
9. Fare clic su **Avanti**.  
  
## <a name="2-choose-the-chart-type"></a><a name="ChartType"></a>2. Scegliere il tipo di grafico  
È possibile scegliere tra diversi tipi predefiniti di grafico, quindi modificare il grafico dopo aver completato la procedura guidata.  
  
### <a name="to-add-a-column-chart"></a>Per aggiungere un istogramma  
  
1.  L'istogramma è il tipo di grafico predefinito nella pagina **Scegliere un tipo di grafico** . Fare clic su **Avanti**.  
  
2.  Nella pagina **Disponi campi del grafico** trascinare il campo SalesDate in **Categorie**. Le categorie vengono visualizzate sull'asse orizzontale.  
  
3.  Trascinare il campo Sales in **Valori**. Nella casella **Valori** viene visualizzato Sum(Sales) perché per ogni data viene aggregata la somma dei totali di vendita. I valori vengono visualizzati sull'asse verticale.  
  
4.  Fare clic su **Avanti**.  
 
6.  Fare clic su **Fine**.  
  
    Il grafico verrà aggiunto all'area di progettazione. Si noti che il nuovo grafico a colonne include solo dati rappresentativi. La legenda visualizza Sales Date A, Sales Date B e così via per dare un'idea dell'aspetto finale del report. 
    
    ![report-builder-column-chart-1-design-view](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. Le dimensioni dell'area di progettazione del report vengono aumentate in base alle dimensioni del grafico.  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  

    ![report-builder-column-chart-1-preview](../reporting-services/media/report-builder-column-chart-1-preview.png)

Osservare che sull'asse orizzontale del grafico non viene assegnata un'etichetta a ogni categoria. Per impostazione predefinita, vengono incluse solo le etichette che possono essere posizionate accanto all'asse. 
  
## <a name="3-format-a-date-on-the-horizontal-axis"></a><a name="Horizontal"></a>3. Formattare una data sull'asse orizzontale  
Per impostazione predefinita, sull'asse orizzontale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sull'asse orizzontale > **Proprietà asse orizzontale**.  
  
3.  Nella scheda **Numero** , in **Categoria**selezionare **Data**.  
  
5.  Nella casella **Tipo** selezionare **31 gennaio 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Nella scheda Home fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
La data viene visualizzata nel formato selezionato. Il grafico continua a non assegnare un'etichetta a ogni categoria dell'asse orizzontale. 

![report-builder-column-chart-2-preview](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
È possibile personalizzare la visualizzazione delle etichette ruotandole e specificando l'intervallo.  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4. Ruotare le etichette asse sull'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sul titolo dell'asse orizzontale, quindi scegliere **Mostra titolo asse** per rimuovere il titolo. Poiché sull'asse orizzontale vengono visualizzate le date, il titolo non è necessario.  
  
3.  Fare clic con il pulsante destro del mouse sull'asse orizzontale > **Proprietà asse orizzontale**.  
  
5.  Nella scheda **Etichette** , in **Modifica opzioni adattamento etichetta asse**selezionare **Disabilita adattamento**.  
  
7.  In **Angolo di rotazione etichetta**selezionare **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Il testo di esempio per l'asse orizzontale ruota di 90 gradi.  
    
    ![report-builder-column-chart-rotate-x-axis](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nel grafico le etichette appaiono ruotate.  

![report-builder-column-chart-rotate-x-axis-preview](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="5-move-the-legend"></a><a name="Legend"></a>5. Spostare la legenda  
La legenda viene creata automaticamente dai dati di categoria e serie. È possibile spostare la legenda al di sotto dell'area del grafico di un istogramma.  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sul grafico > **Proprietà legenda**.  
  
3.  In **Layout e posizione**selezionare una posizione diversa. Ad esempio, selezionare l'opzione centrale inferiore.  
  
    Quando la legenda viene posizionata alla fine o all'inizio di un grafico, il relativo layout viene modificato da verticale in orizzontale. È possibile selezionare un altro layout nella casella **Layout** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Facoltativo) Poiché in questa esercitazione è presente una sola categoria, il grafico non richiede una legenda. Fare clic con il pulsante destro del mouse sulla legenda > **Elimina legenda**.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="6-title-the-chart"></a><a name="ChartTitle"></a>6. Spostare il titolo del grafico  
    
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Selezionare le parole **Titolo grafico** nella parte superiore del grafico, quindi digitare **Totali ordini di vendita negozi**.  
  
3.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="7-format-and-label-the-vertical-axis"></a><a name="Vertical"></a>7. Formattare l'asse verticale e assegnare un'etichetta  
Per impostazione predefinita, sull'asse verticale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.   
  
1.  Passare alla visualizzazione di progettazione report.  
  
2. Fare clic sulle etichette dell'asse verticale sul lato sinistro del grafico per selezionarle.  
  
3.  Nella scheda **Home** > gruppo **Numero** fare clic sul pulsante **Valuta**. Le etichette dell'asse cambiano per mostrare il formato della valuta.  
  
4.  Fare clic due volte sul pulsante **Diminuisci decimali** per visualizzare il numero arrotondato al dollaro più vicino.  
  
5.  Fare clic con il pulsante destro del mouse sull'asse verticale > **Proprietà asse verticale**.  
  
6.  Nella scheda **Numero** osservare che **Valuta** è già selezionata nella casella **Categoria** e che in **Cifre decimali** è già indicato **0** (zero).  
  
7.  Selezionare **Mostra valori in**. L'opzione**Migliaia** è già selezionata.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare clic con il pulsante destro del mouse sull'asse verticale > **Mostra titolo asse**. 

10. Fare clic con il pulsante destro del mouse sul titolo dell'asse verticale > **Proprietà titolo asse**.  
  
10. Sostituire il testo nel campo **Testo titolo** con il testo **Totale vendite (in migliaia)** . È anche possibile specificare diverse opzioni relative alla formattazione del titolo.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Fare clic su **Esegui** per visualizzare l'anteprima del report.  

    ![report-builder-column-chart-format-y-axis](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8. Visualizzare tutte le etichette sull'asse orizzontale (x)

Si noti che sull'asse x sono visualizzate solo alcune etichette. In questa sezione si imposterà una proprietà nel riquadro Proprietà per visualizzare tutte le etichette.

1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sul grafico, quindi selezionare le etichette dell'asse orizzontale.

3. Nel riquadro Proprietà impostare LabelInterval su 1.

    ![report-builder-column-chart-set-label-interval](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    Il grafico ha lo stesso aspetto nella visualizzazione Progettazione. 
    
5.  Fare clic su **Esegui** per visualizzare l'anteprima del report.

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Ora il grafico visualizza tutte le etichette.
  
## <a name="9-add-a-moving-average-with-a-calculated-series"></a><a name="Average"></a>9. Aggiungere una media mobile con una serie calcolata  

Una media mobile è una media dei dati della serie calcolata nel tempo. La media mobile favorisce l'identificazione delle tendenze.
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Fare clic con il pulsante destro del mouse sul campo **[Sum(Sales)]** disponibile nell'area **Valori** , quindi scegliere **Aggiungi serie calcolata**.  

     ![report-builder-column-chart-add-calculated-series](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  In **Formula**verificare che sia selezionata l'opzione **Media mobile** .  
  
5.  In **Imposta parametri formula**, per l'opzione **Periodo**selezionare **4**.  
  
6.  Nella scheda **Bordo** , in **Spessore linea**selezionare **3pt**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nel grafico viene visualizzata una riga in cui è riportata la media mobile delle vendite totali per data, calcolata in base a un intervallo di quattro date. Ulteriori informazioni sull' [aggiunta di una media mobile a un grafico](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md). 

![report-builder-column-chart-moving-average](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="10-add-a-report-title"></a><a name="Title"></a>10. Aggiungere un titolo al report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
3.  Digitare **Grafico a barre - Vendite**, premere INVIO, quindi digitare **Gennaio - dicembre 2015**in modo da ottenere un risultato simile al seguente:  
  
    **Grafico a barre - Vendite**  
  
    **Gennaio - dicembre 2015**  
  
4.  Selezionare **Grafico a barre - Vendite**, quindi nella scheda **Home** > sezione **Carattere** > **Grassetto**.  
  
5.  Selezionare **Gennaio - dicembre 2015** e nella scheda **Home** > sezione **Carattere** > impostare le dimensioni del carattere su **10**.  
  
6.  (Facoltativo) Per contenere le due righe del testo potrebbe essere necessario aumentare l'altezza della casella di testo **Titolo** . Tirare verso il basso le doppie frecce quando si fa clic al centro del bordo inferiore. Può anche essere necessario trascinare la parte superiore del grafico in modo che il titolo non si sovrapponga.  
  
    Il titolo viene visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="11-save-the-report"></a><a name="Save"></a>11. Salvare il report  
  
### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Dal pulsante Generatore report fare clic su **Salva con nome**.  

    È possibile salvarlo nel computer o nel server di report.
  
3.  In **Nome**digitare **Istogramma ordini vendita**.  
  
4.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
Questo passaggio conclude l'esercitazione relativa all'aggiunta di un istogramma al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
-    [Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md) 
-    [Generatore report in SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

