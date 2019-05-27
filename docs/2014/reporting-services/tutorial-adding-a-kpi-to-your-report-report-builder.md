---
title: 'Esercitazione: Aggiunta di un indicatore di prestazioni chiave al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a1b158b6fc504a0917e0c268846da93be3aa59b9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66098980"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Esercitazione: Aggiunta di un indicatore di prestazioni chiave al report (Generatore report)
  Un indicatore di prestazioni di chiave (KPI) è un valore misurabile dotato di significato aziendale. In questa esercitazione verrà illustrato come includere un indicatore KPI in un report. In questo scenario l'indicatore KPI è il riepilogo delle vendite in base alle sottocategorie del prodotto. Lo stato corrente dell'indicatore KPI viene mostrato tramite colori, misuratori e indicatori.  
  
 Nell'illustrazione seguente viene mostrato il report che verrà creato.  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
 In questa esercitazione verrà illustrato come aggiungere un indicatore KPI impostando il colore di sfondo delle celle della tabella in base al valore della cella, nonché come aggiungere e configurare un misuratore e un indicatore. Verrà inoltre illustrato come scrivere l'espressione che consente di impostare il colore di sfondo delle celle della tabella.  
  
 In questa esercitazione sono disponibili le procedure seguenti:  
  
1.  [Creare un Report tabella e un set di dati dalla tabella o dalla creazione guidata matrice](#Table)  
  
2.  [Organizzare i dati, scegliere il Layout e lo stile dalla tabella o procedura guidata matrice](#CompleteWizard)  
  
3.  [Utilizzare i colori di sfondo per visualizzare un indicatore KPI](#BackgroundColors)  
  
4.  [Visualizzare un indicatore KPI tramite un misuratore](#Gauge)  
  
5.  [Visualizzare un indicatore KPI tramite un indicatore](#Indicator)  
  
6.  [Aggiungere un titolo al Report](#Title)  
  
7.  [Salvare il Report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi della procedura guidata sono consolidati in due procedure: una per la creazione del set di dati e un'altra per la creazione di una tabella. Per istruzioni dettagliate su come selezionare un server di report, scegliere un'origine dati, creare un set di dati ed eseguire la procedura guidata. Vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo stimato per completare questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Table"></a> 1. Creare un report tabella e un set di dati dalla Creazione guidata tabella o matrice  
 Dal **introduttiva** finestra di dialogo, scegliere un'origine dati condivisa, creare un set di dati incorporato e visualizzare i dati in una tabella.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-table"></a>Per creare una nuova tabella  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** .  
  
    > [!NOTE]  
    >  Se il **Guida introduttiva** non viene visualizzato nella finestra di dialogo, dal pulsante Generatore Report, fare clic su **New**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro fare clic su **Creazione guidata tabella o matrice**.  
  
4.  Nella pagina scegliere un set di dati, fare clic su **creare un set di dati**.  
  
5.  Scegliere **Avanti**.  
  
6.  Nella pagina **Scegliere una connessione a un'origine dei dati** selezionare un'origine dati esistente o individuare il server di report e selezionare un'origine dati. Se non vi è alcuna origine dati disponibile o non si dispone dell'accesso a un server di report, è possibile utilizzare un'origine dati incorporata. Per altre informazioni, vedere [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
9. Copiare e incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. Scegliere **Avanti**.  
  
##  <a name="CompleteWizard"></a> 2. Organizzare i dati, scegliere il Layout e lo stile dalla tabella o procedura guidata matrice  
 Utilizzare la procedura guidata per fornire una progettazione iniziale in cui visualizzare i dati. Il riquadro di anteprima nella procedura guidata consente di visualizzare il risultato del raggruppamento di dati prima di completare la progettazione della tabella o della matrice.  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>Per organizzare i dati in gruppi, scegliere un layout e uno stile  
  
1.  Nella pagina Disponi campi trascinare Product in **Valori**.  
  
2.  Trascinare Quantity in **Valori** e posizionarlo sotto Product.  
  
     Il campo Quantity viene riepilogato con la funzione Sum, ovvero la funzione predefinita per riepilogare i campi numerici.  
  
3.  Trascinare Sales in **Valori** e posizionarlo sotto Quantity.  
  
     Nei passaggi 1, 2 e 3 sono specificati i dati da visualizzare nella tabella.  
  
4.  Trascinare SalesDate in **Gruppi di righe**.  
  
5.  Trascinare Subcategory in **Gruppi di righe** e posizionarlo sotto SalesDate.  
  
     I passaggi 4 e 5 consentono di organizzare i valori per i campi prima in base alla data, quindi in base a tutte le vendite per tale data.  
  
6.  Scegliere **Avanti**.  
  
     Quando si esegue il report, nella tabella vengono visualizzati tutte le date, tutti gli ordini per ciascuna data e tutti i prodotti, le quantità e i totali di vendite per ogni ordine.  
  
7.  Nella pagina Scegliere il layout, in **Opzioni**, verificare che la casella **Mostra subtotali e totali complessivi** sia selezionata.  
  
8.  Verificare che l'opzione **Bloccato, subtotale sotto** sia selezionata.  
  
9. Deselezionare l'opzione **Espandi/comprimi gruppi**.  
  
     Nel report creato in questa esercitazione non viene utilizzata la funzionalità drill-down che consente all'utente di espandere una gerarchia di gruppo padre per visualizzare le righe del gruppo figlio e le righe di dettaglio.  
  
10. Scegliere **Avanti**.  
  
11. Selezionare uno stile dal riquadro Stili della pagina Scegliere uno stile.  
  
     Lo stile utilizzato nell'illustrazione per il record completato è Oceano.  
  
12. Scegliere **Fine**.  
  
     La tabella viene aggiunta all'area di progettazione. Nella tabella sono presenti cinque colonne e altrettante righe. Nel riquadro Gruppi di righe vengono visualizzati tre gruppi di righe: SalesDate, Subcategory e Details. I dati dettaglio costituiscono tutti i dati recuperati dalla query del set di dati.  
  
13. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Per ogni prodotto venduto in una data specifica, nella tabella vengono visualizzati il nome del prodotto, la quantità venduta e il totale delle vendite. I dati sono organizzati prima in base alla data delle vendite, quindi in base alla sottocategoria.  
  
##  <a name="BackgroundColors"></a> 3. Utilizzare i colori di sfondo per visualizzare un indicatore KPI  
 I colori di sfondo possono essere impostati su un'espressione valutata quando si esegue il report.  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando i colori di sfondo  
  
1.  Nella tabella, fare doppio clic su due celle verso il basso dal `[Sum(Sales)]` cella (riga del subtotale che visualizza le vendite per una sottocategoria) e quindi fare clic su **proprietà casella di testo**.  
  
2.  In **riempire**, fare clic sul **fx** accanto al **colore di riempimento** l'opzione e immettere l'espressione seguente nella **imposta espressione per: BackgroundColor**.  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 Il colore di sfondo cambierà in verde, utilizzando la sfumatura di verde denominata "Verde brillante", per ogni cella contenente una somma aggregata per `[Sum(Sales)]` che può essere maggiore o uguale a 5000. I valori di `[Sum(Sales)]` compresi tra 2500 e 5000 sono visualizzati in giallo, mentre quelli minori di 2500 in rosso.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nella riga del subtotale in cui sono visualizzate le vendite per una sottocategoria, il colore di sfondo della cella è rosso, giallo o verde a seconda del valore della somma delle vendite.  
  
##  <a name="Gauge"></a> 4. Visualizzare un indicatore KPI tramite un misuratore  
 Un misuratore raffigura un singolo valore di un set di dati. In questa esercitazione viene utilizzato un misuratore lineare orizzontale poiché la relativa forma e semplicità ne rende facile la lettura, anche quando è di piccole dimensioni e viene utilizzato all'interno di una cella della tabella. Per altre informazioni, vedere [Misuratori &#40;Generatore report e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando un misuratore  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nella tabella, fare clic sul gestore della colonna per la cella modificata nella procedura precedente, scegliere **Inserisci colonna**, quindi fare clic su **destra**. Alla tabella verrà aggiunta una nuova colonna.  
  
3.  Tipo di **KPI** nell'intestazione di colonna.  
  
4.  Nel **inserire** nella scheda il **aree dati** fare clic su **misuratore**e quindi fare clic nell'area di progettazione esterna alla tabella. Verrà visualizzata la finestra di dialogo **Seleziona tipo di misuratore** .  
  
5.  Fare clic su **lineare**. Il primo tipo di misuratore lineare **orizzontale**, sia selezionata.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Nell'area di progettazione verrà aggiunto un misuratore.  
  
7.  Dal riquadro dei dati del report trascinare Sales nel misuratore. Quando si trascina Sales nel misuratore, viene visualizzato il riquadro Dati misuratore.  
  
8.  Rilasciare Sales nel **valori** elenco.  
  
     Quando si rilascia il campo nel misuratore, il campo viene aggregato utilizzando la funzione Sum predefinita.  
  
9. Fare doppio clic il puntatore nel misuratore e scegliere **proprietà indicatore di misura**.  
  
10. Nelle **tipo di puntatore**, selezionare **barra**. L'indicatore di misura si trasformerà da marcatore in una barra che risulterà più visibile in seguito all'aggiunta del misuratore alla tabella.  
  
11. Fare clic su **riempimento puntatore**. Nelle **colore secondario** prelievo **giallo**. Il modello di riempimento sfumato cambierà da bianco in giallo.  
  
12. Fare clic con il pulsante destro del mouse sulla scala nel misuratore e selezionare **Proprietà scala**.  
  
13. Impostare il **massimo** opzione su 25000.  
  
    > [!NOTE]  
    >  Per calcolare dinamicamente il valore dell'opzione **Massimo** è possibile usare un'espressione invece di una costante, ad esempio 25000. L'espressione utilizzerebbe in tal caso l'aggregazione della funzionalità di aggregazione, rendendola simile all'espressione `=Max(Sum(Fields!Sales.value), "Tablix1")`.  
  
14. Trascinare il misuratore all'interno della tabella, nella terza cella della riga del subtotale in cui sono visualizzate le vendite per una sottocategoria della colonna inserita.  
  
    > [!NOTE]  
    >  Potrebbe essere necessario ridimensionare la colonna in modo che il misuratore lineare orizzontale rientri nella cella. Per ridimensionare la colonna, fare clic sull'intestazione e utilizzare gli handle per ridimensionare le celle orizzontalmente e verticalmente.  
  
15. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
     La lunghezza orizzontale della barra nel misuratore cambia in base al valore dell'indicatore KPI.  
  
16. (Facoltativo) Aggiungere un pin massimo per gestire l'overflow in modo che qualsiasi valore che supera il massimo della scala punti sempre al pin massimo:  
  
    1.  Aprire il riquadro Proprietà.  
  
    2.  Fare clic sulla scala. Le proprietà della scala lineare verranno visualizzate nel riquadro Proprietà.  
  
    3.  Nel **PIN della scala** categoria, espandere il **MaximumPin** nodo.  
  
    4.  Impostare il **abilitare** proprietà `True`. Verrà visualizzato un pin dopo il valore massimo della scala.  
  
    5.  Impostare **BorderColor** a `Lime`.  
  
17. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Indicator"></a> 5. Visualizzare un indicatore KPI tramite un indicatore  
 Gli indicatori sono piccoli e semplici misuratori che consentono di visualizzare i valori dei dati in modo immediato. Grazie alle loro dimensioni e alla semplicità, gli indicatori vengono spesso utilizzati nelle tabelle e nelle matrici. Per altre informazioni, vedere [Indicatori &#40;Generatore report e SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando un indicatore  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nella tabella, fare clic sul gestore della colonna per la cella modificata nella procedura precedente, scegliere **Inserisci colonna**, quindi fare clic su **destra**. Alla tabella verrà aggiunta una nuova colonna.  
  
3.  Tipo di **KPI** nell'intestazione di colonna.  
  
4.  Fare clic sulla cella per il subtotale della sottocategoria.  
  
5.  Nel **inserire** nella scheda il **aree dati** gruppo, fare doppio clic su **indicatore.**  
  
     Verrà visualizzata la finestra di dialogo **Seleziona tipo indicatore** .  
  
6.  Fare clic su **forme**. Il primo tipo di forma **3 semafori (senza bordo),** sia selezionata.  
  
     Nell'esercitazione verrà utilizzato questo indicatore.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     L'indicatore verrà aggiunto all'area di progettazione.  
  
8.  Fare clic con il pulsante destro del mouse sull'indicatore e scegliere **Proprietà indicatore**.  
  
9. Fare clic su **valori e stati**.  
  
10. Nell'elenco a discesa dei valori, selezionare **[SUM (Sales)]**, ma non modificare eventuali altre opzioni.  
  
     Per impostazione predefinita, si verifica la sincronizzazione dei dati nell'area dati e il valore **Tablix1**, ovvero il nome dell'area dati della tabella nel report, viene visualizzato nella casella **Ambito sincronizzazione** .  
  
     In questo report, è possibile anche modificare l'ambito di un indicatore posizionato nella cella del subtotale della sottocategoria per eseguire la sincronizzazione nel campo SalesDate.  
  
11. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Title"></a> 6. Aggiungere un titolo al report  
 Nella parte superiore del report viene visualizzato il titolo del report. È possibile posizionare il titolo del report in un'apposita intestazione oppure, se ne è privo, in una casella di testo nella parte superiore del corpo del report. Sarà utilizzata la casella di testo che viene posizionata automaticamente nella parte superiore del corpo del report.  
  
 Il testo può essere ulteriormente migliorato applicando stili di carattere, dimensioni e colori diversi alle frasi e ai singoli caratteri del testo. Per altre informazioni, vedere [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Tipo di **KPI vendite prodotto**e quindi fare clic all'esterno della casella di testo.  
  
3.  Facoltativamente, fare clic sulla casella di testo che contiene **KPI vendite prodotto**, fare clic su **proprietà casella di testo**e quindi nella scheda carattere scegliere i diversi stili di carattere, dimensioni e colori.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Save"></a> 7. Salvare il report  
 Salvare il report in un server di report o nel computer. Se il report non viene salvato nel server di report, non saranno disponibili alcune funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , ad esempio le parti del report e i sottoreport.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
     Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con **Product Sales KPI**.  
  
5.  Fare clic su **Salva**.  
  
 Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**e selezionare la cartella in cui si vuole salvare il report.  
  
> [!NOTE]  
>  Se non si ha accesso a un server di report, fare clic su **Desktop**, **Documenti**o **Risorse del computer** e salvare il report nel computer.  
  
1.  In **Nome**sostituire il nome predefinito con **Product Sales KPI**.  
  
2.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questo passaggio conclude l'esercitazione relativa all'aggiunta di un indicatore KPI al report. Per altre informazioni, vedere misuratori (Generatore Report) [gli indicatori di &#40;Generatore Report e SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
