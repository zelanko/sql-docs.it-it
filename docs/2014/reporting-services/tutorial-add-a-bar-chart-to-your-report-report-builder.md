---
title: 'Esercitazione: Aggiungere un grafico a barre al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b21826cb926dbd5f8b0315f490b20850c6ccd23
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62648317"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un grafico a barre al report (Generatore report)
  In un grafico a barre i dati delle categorie vengono visualizzati orizzontalmente per gli scopi seguenti:  
  
-   Migliorare la leggibilità dei nomi di categoria lunghi.  
  
-   Migliorare la comprensibilità delle ore tracciate come valori.  
  
-   Confrontare il valore relativo di più serie.  
  
 Nell'illustrazione seguente viene mostrato il grafico a barre che verrà creato, in ordine alfabetico, con le vendite dei primi cinque venditori per gli anni 2008 e 2009.  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
1.  [Creare un grafico da Creazione guidata grafico](#Chart)  
  
2.  [Scegliere il tipo di grafico](#ChartType)  
  
3.  [Visualizzare tutti i valori di categorie sull'asse verticale](#AllValues)  
  
4.  [Modificare la visualizzazione dei nomi sull'asse verticale](#Sort)  
  
5.  [Spostare la legenda](#Legend)  
  
6.  [Spostare il titolo del grafico](#ChartTitle)  
  
7.  [Formattare e assegnare un'etichetta asse orizzontale](#Horizontal)  
  
8.  [Aggiungere un filtro per visualizzare i primi cinque valori](#Filter)  
  
9. [Aggiungere un titolo al Report](#Title)  
  
10. [Salvare il Report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, creare un set di dati e scegliere un'origine dati. Vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo stimato per completare questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Creare un report grafico da Creazione guidata grafico  
 Dal **introduttiva** nella finestra di dialogo Crea un set di dati incorporato, scegliere un'origine dati condivisa e creare un grafico a barre tramite Creazione guidata grafico.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-chart-report"></a>Per creare un nuovo report grafico  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** .  
  
    > [!NOTE]  
    >  Se il **Guida introduttiva** finestra di dialogo non vengono visualizzati, fare clic sul pulsante Generatore Report e quindi fare clic su **New**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**e fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    >  L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati sui quali verrà basato il grafico.  
  
9. Scegliere **Avanti**.  
  
##  <a name="ChartType"></a> 2. Scegliere il tipo di grafico  
 È possibile scegliere tra diversi tipi di grafico predefiniti.  
  
#### <a name="to-add-a-column-chart"></a>Per aggiungere un istogramma  
  
1.  L'istogramma è il tipo di grafico predefinito nella pagina **Scegliere un tipo di grafico** .  
  
2.  Fare clic su **Barre**, quindi su **Avanti**.  
  
     Nel riquadro **Campi disponibili** della pagina **Disponi campi del grafico** sono contenuti quattro campi: FirstName, LastName, SalesYear2009 e SalesYear2008.  
  
3.  Trascinare LastName nel riquadro Categorie.  
  
4.  Trascinare SalesYear2009 nel riquadro Valori. SalesYear2009 rappresenta l'importo delle vendite di ogni venditore per l'anno 2009. Nel riquadro Valori viene visualizzato `[Sum(SalesYear2009)]` perché nel grafico viene mostrata l'aggregazione per ogni prodotto.  
  
5.  Trascinare SalesYear2008 nel riquadro Valori sotto SalesYear2009. SalesYear2008 rappresenta l'importo delle vendite di ogni venditore per l'anno 2008.  
  
6.  Scegliere **Avanti**.  
  
7.  Nel **scegliere uno stile** pagina, selezionare uno stile nel riquadro stili.  
  
     Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo. Quando si seleziona uno stile, nel riquadro di anteprima viene visualizzato un esempio del grafico con lo stile selezionato.  
  
8.  Scegliere **Fine**.  
  
     Il grafico verrà aggiunto all'area di progettazione.  
  
9. Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo.  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report viene visualizzato il grafico a barre relativo alle vendite di ogni venditore per gli anni 2008 e 2009. La lunghezza della barra corrisponde al totale delle vendite.  
  
##  <a name="AllValues"></a> 3. Modificare la visualizzazione dei nomi sull'asse verticale  
 Per impostazione predefinita sull'asse verticale vengono visualizzati solo alcuni valori. È possibile modificare il grafico per visualizzare tutte le categorie.  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>Per visualizzare tutti i venditori lungo l'asse delle categorie di un grafico a barre  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic dell'asse verticale e quindi fare clic su **proprietà asse verticale**.  
  
3.  Nella casella **Intervallo**di **Intervallo asse** digitare **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare doppio clic su verticale **titolo asse** e deselezionare le **Mostra titolo asse** casella di controllo.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
> [!NOTE]  
>  Se i nomi dei venditori sull'asse verticale non sono leggibili, è possibile aumentare l'altezza del grafico o modificare le opzioni di formattazione per le etichette dell'asse.  
  
###  <a name="CategoryExpression"></a> Visualizzare cognome e nome sull'asse verticale  
 È possibile modificare l'espressione delle categorie per includere il cognome seguito dal nome di ogni venditore.  
  
##### <a name="to-change-the-category-expression"></a>Per modificare l'espressione delle categorie  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  In Etichetta fare clic sul pulsante espressione (Fx).  
  
5.  Digitare l'espressione seguente: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
     Questa espressione determina la concatenazione di cognome, virgola e nome.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Se i nomi non vengono visualizzati quando si esegue il report, è possibile aggiornare i dati manualmente. Mentre si è ancora in modalità anteprima, fare clic su **Aggiorna** nel gruppo **Navigazione** della scheda **Esegui**.  
  
> [!NOTE]  
>  Se i nomi dei venditori sull'asse verticale non sono leggibili, è possibile aumentare l'altezza del grafico o modificare le opzioni di formattazione per le etichette dell'asse.  
  
##  <a name="Sort"></a> 4. Modificare l'ordinamento per i nomi sull'asse verticale  
 Quando si ordinano i dati in un grafico si modifica l'ordine dei valori sull'asse delle categorie.  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>Per ordinare i nomi in ordine alfabetico sul grafico a barre  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  Fare clic su **Ordinamento**. Nella pagina **Modificare le opzioni di ordinamento** viene visualizzato un elenco di espressioni di ordinamento. Per impostazione predefinita, l'elenco dispone di un'unica espressione di ordinamento che equivale all'espressione originale di raggruppamento delle categorie.  
  
5.  In Ordina per scegliere l'espressione (**Fx**) pulsante.  
  
6.  Digitare l'espressione seguente: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  Fare clic su **OK**.  
  
8.  Riaccenderle il **proprietà gruppo categorie** pagina il **ordine** elenco a discesa, seleziona **dalla Z alla A**. Ciò consente di selezionare ordine alfabetico inverso in modo che i nomi visualizzati nell'ordine dall'alto verso il basso.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I nomi sull'asse orizzontale vengono ordinati in ordine inverso, partendo **Alerca** nella parte superiore e **Zeng** nella parte inferiore.  
  
##  <a name="Legend"></a> 5. Spostare la legenda  
 Per migliorare la leggibilità dei valori del grafico, è possibile spostare la legenda del grafico. In un grafico a barre in cui le barre sono visualizzate orizzontalmente, è ad esempio possibile modificare la posizione della legenda in modo che si trovi al di sopra o al di sotto dell'area del grafico. In questo modo lo spazio orizzontale disponibile per le barre risulterà maggiore.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Per visualizzare la legenda al di sotto dell'area del grafico di un grafico a barre  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sulla legenda nel grafico.  
  
3.  Selezionare **Proprietà legenda**.  
  
4.  In **Posizione legenda**selezionare un'altra posizione, ad esempio la posizione centrale inferiore.  
  
     Quando la legenda viene posizionata alla fine o all'inizio di un grafico, il relativo layout viene modificato da verticale in orizzontale. È possibile selezionare un altro layout nell'elenco a discesa **Layout** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="ChartTitle"></a> 6. Spostare il titolo del grafico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>Per modificare il titolo di un grafico a barre al di sopra dell'area del grafico  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Selezionare le parole **titolo del grafico** nella parte superiore del grafico e quindi digitare il testo seguente: **Vendite per 2008 e 2009**.  
  
3.  Fare clic in un punto qualsiasi all'esterno del testo.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Horizontal"></a> 7. Formattare l'asse orizzontale e assegnare un'etichetta  
 Per impostazione predefinita, sull'asse orizzontale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico.  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>Per formattare i numeri sull'asse orizzontale  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sull'asse orizzontale lungo il bordo inferiore del grafico per selezionarlo.  
  
     Sulla barra multifunzione, nel **Home** nella scheda il **numero** raggruppare, fare clic il **valuta** pulsante. Le etichette dell'asse orizzontale vengono convertite nel formato valuta.  
  
3.  (Facoltativo) Rimuovere le cifre decimali. Fare clic due volte sul pulsante **Diminuisci decimali** accanto al pulsante **Valuta** .  
  
4.  Fare clic con il pulsante destro del mouse sull'asse orizzontale e scegliere **Proprietà asse orizzontale**.  
  
5.  Nel **numero** scheda, seleziona **Mostra valori in migliaia.**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Fare doppio clic su **titolo asse** e fare clic su **proprietà titolo asse**.  
  
8.  Nel **testo titolo** , digitare **vendite in migliaia** e fare clic su **OK**.  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report l'importo delle vendite viene visualizzato sull'asse orizzontale come valuta in migliaia senza cifre decimali.  
  
##  <a name="Filter"></a> 8. Aggiungere un filtro per visualizzare i primi cinque valori  
 È possibile aggiungere un filtro al grafico per specificare quali dati del set di dati includere o escludere.  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>Per aggiungere un filtro e visualizzare i primi cinque valori  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  Fare clic su **Filtri**. Nella pagina **Modificare i filtri** può essere visualizzato un elenco di espressioni di filtro. Per impostazione predefinita, tale elenco è vuoto.  
  
5.  Scegliere **Aggiungi**. Verrà visualizzato un nuovo filtro vuoto.  
  
6.  Nelle **espressione**, digitare **[Sum(SalesYear2009)]**. Viene creata l'espressione sottostante `=Sum(Fields!SalesYear2009.Value)`, che può essere visualizzata facendo clic sul pulsante **fx** .  
  
7.  Verificare che il tipo di dati sia **Text**.  
  
8.  In **Operatore**selezionare **Top N** nell'elenco a discesa.  
  
9. In **Valore**digitare l'espressione seguente: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Se i risultati non vengono filtrati quando si esegue il report, sarà possibile aggiornare i dati manualmente. Nella scheda **Esegui** del gruppo **Navigazione** fare clic su **Aggiorna**.  
  
 Nel grafico verranno visualizzati i primi cinque nomi di venditori in base ai dati relativi alle vendite del 2009.  
  
##  <a name="Title"></a> 9. Aggiungere un titolo al report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Tipo di **grafico a barre-vendite**, premere INVIO e quindi digitare **primi cinque venditori per 2009**, in modo che risulti simile al seguente:  
  
     **Grafico a barre - Vendite**  
  
     **Primi cinque venditori per 2009**  
  
3.  Selezionare **Grafico a barre - Vendite**e fare clic sul pulsante **Grassetto** .  
  
4.  Selezionare **primi cinque venditori per 2009**e il **Font** sezione il **Home** scheda, impostare la dimensione del carattere su **10**.  
  
5.  (Facoltativo) Per contenere le due righe del testo potrebbe essere necessario aumentare l'altezza della casella di testo Titolo.  
  
     Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Save"></a> 10. Salvare il report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
3.  In **Nome**digitare **Grafico a barre - Vendite**.  
  
4.  Fare clic su **Salva**.  
  
 Il report verrà salvato sul server di report.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un grafico a barre al report. Per altre informazioni sui grafici, vedere [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) e [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
