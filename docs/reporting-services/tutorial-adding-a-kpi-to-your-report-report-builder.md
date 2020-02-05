---
title: 'Esercitazione: Aggiunta di un indicatore di prestazioni chiave al report (Generatore report) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ee2333bc6d369bbc9908198d8cfa2fa18ce23065
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63041891"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Esercitazione: Aggiunta di un indicatore di prestazioni chiave al report (Generatore report)
In questa esercitazione di [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] si aggiunge un indicatore di prestazioni chiave (KPI) a un report impaginato di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)].  

Gli indicatori KPI sono valori misurabili con significato aziendale. In questo scenario l'indicatore KPI è il riepilogo delle vendite in base alle sottocategorie del prodotto. Lo stato corrente dell'indicatore KPI viene indicato da colori, misuratori e indicatori.
  
L'immagine seguente illustra un report simile quello che verrà creato.  
  
![report-builder-kpi-report](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> In questa esercitazione, i passaggi della procedura guidata sono consolidati in due procedure: una per la creazione del set di dati e un'altra per la creazione di una tabella. Per istruzioni dettagliate su come selezionare un server di report, scegliere un'origine dati, creare un set di dati ed eseguire la procedura guidata, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo previsto per il completamento di questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Table"></a>1. Creare un report tabella e un set di dati dalla Creazione guidata tabella o matrice  
Questa sezione spiega come scegliere un'origine dati condivisa, creare un set di dati incorporato e visualizzare i dati in una tabella.  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>Per creare una tabella con un set di dati incorporato  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal computer, dal portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o in modalità integrata SharePoint.  
  
    Si apre la finestra di dialogo **Nuovo report o set di dati** .  
  
    Se la finestra di dialogo **Nuovo report o set di dati** non viene visualizzata, scegliere **Nuovo** dal menu **File**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro fare clic su **Creazione guidata tabella o matrice**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**.  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **Scegliere una connessione a un'origine dei dati** selezionare un'origine dati esistente o individuare il server di report e selezionare un'origine dati. Se non vi è alcuna origine dati disponibile o non si dispone dell'accesso a un server di report, è possibile utilizzare un'origine dati incorporata. Per altre informazioni, vedere [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
9. Copiare e incollare la query seguente nel relativo riquadro:  

    > [!NOTE]  
    > Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. Sulla barra degli strumenti Progettazione query fare clic su Esegui ( **!** ).

11. Fare clic su **Avanti**.  
  
## <a name="CompleteWizard"></a>2. Organizzare i dati e scegliere il layout nella procedura guidata  
La Creazione guidata tabella o matrice offre una progettazione iniziale in cui visualizzare i dati. Il riquadro di anteprima nella procedura guidata consente di visualizzare il risultato del raggruppamento di dati prima di completare la progettazione della tabella o della matrice.  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>Per organizzare i dati in gruppi e scegliere un layout 
  
1.  Nella pagina Disponi campi trascinare Product in **Valori**.  
  
2.  Trascinare Quantity in **Valori** e posizionarlo sotto Product.  
  
    Il campo Quantity viene riepilogato con la funzione Sum, ovvero la funzione predefinita per riepilogare i campi numerici.  
  
3.  Trascinare Sales in **Valori** e posizionarlo sotto Quantity.  
  
    Nei passaggi 1, 2 e 3 sono specificati i dati da visualizzare nella tabella.  
  
4.  Trascinare SalesDate in **Gruppi di righe**.  
  
5.  Trascinare Subcategory in **Gruppi di righe** e posizionarlo sotto SalesDate.  
  
    I passaggi 4 e 5 consentono di organizzare i valori per i campi prima in base alla data, quindi in base a tutte le vendite per tale data.  
  
6.  Fare clic su **Avanti**.  
  
    Quando si esegue il report, nella tabella vengono visualizzati tutte le date, tutti gli ordini per ciascuna data e tutti i prodotti, le quantità e i totali di vendite per ogni ordine.  
  
7.  Nella pagina Scegliere il layout, in **Opzioni**, verificare che la casella **Mostra subtotali e totali complessivi** sia selezionata.  
  
8.  Verificare che l'opzione **Bloccato, subtotale sotto** sia selezionata.  
  
9. Deselezionare l'opzione **Espandi/comprimi gruppi**.  
  
    Nel report creato in questa esercitazione non viene utilizzata la funzionalità drill-down che consente all'utente di espandere una gerarchia di gruppo padre per visualizzare le righe del gruppo figlio e le righe di dettaglio.  
  
10. Fare clic su **Avanti**.  
  
11. Fare clic su **Fine**.  
  
      La tabella viene aggiunta all'area di progettazione. Nella tabella sono presenti cinque colonne e altrettante righe. Nel riquadro Gruppi di righe sono visualizzati tre gruppi di righe: SalesDate, Subcategory e Details. I dati dettaglio costituiscono tutti i dati recuperati dalla query del set di dati. Il riquadro Gruppi di colonne è vuoto.  
      
      ![report-builder-kpi-row-groups](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Per ogni prodotto venduto in una data specifica, nella tabella vengono visualizzati il nome del prodotto, la quantità venduta e il totale delle vendite. I dati sono organizzati prima in base alla data delle vendite, quindi in base alla sottocategoria. 

![report-builder-kpi-basic-table](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>Formattare date e valuta
Allargare le colonne e impostare il formato per date e valuta.

1. Fare clic su **Progettazione** per tornare alla visualizzazione della struttura.

2. Per i nomi di prodotto potrebbe essere necessario più spazio. Per allargare la colonna relativa al prodotto, selezionare l'intera tabella e trascinare il bordo destro del quadratino della colonna nella parte superiore della colonna contenente il prodotto.

3. Premere CTRL e selezionare le quattro celle contenenti [Sum(Sales)].

4. Nella scheda **Home** > **Numero** > **Valuta**. Nelle celle i numeri vengono visualizzati nel formato di valuta.

   Se la lingua delle impostazioni locali è inglese (Stati Uniti), il testo di esempio predefinito sarà [$12,345.00]. Se non viene visualizzato un valore di valuta di esempio, fare clic su **Stili segnaposto** Valori di esempio **nel gruppo** > **Numeri**.
    
    ![report-generatore-segnaposto-valore-pulsante](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (Facoltativo) Nel gruppo **Numero** della scheda **Home** fare clic due volte sul pulsante **Diminuisci decimali** per visualizzare le cifre in dollari senza centesimi.

6. Fare clic sulla cella contenente [SalesDate].

6. Nel gruppo **Numero** > **Data**.

   Nella cella verrà visualizzata la data di esempio [1/31/2000]. 

12. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
 
![report-builder-kpi-format-numbers](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3. Utilizzare i colori di sfondo per visualizzare un indicatore KPI  
I colori di sfondo possono essere impostati su un'espressione valutata quando si esegue il report.  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando i colori di sfondo  
  
1.  Nella tabella fare clic con il pulsante destro del mouse sulla cella `[Sum(Sales)]` (riga del subtotale in cui vengono visualizzate le vendite per una sottocategoria) e scegliere **Proprietà casella di testo**. 

    Assicurarsi di aver selezionato la cella e non il testo per visualizzare **Proprietà casella di testo**. 
    
    ![report-builder-text-box-properties](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  Nella scheda **Riempimento** fare clic sul pulsante **fx** accanto all'opzione **Colore riempimento** e immettere l'espressione seguente nel campo **Imposta espressione per: BackgroundColor** :  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     Lo sfondo di ogni cella con somma aggregata per `[Sum(Sales)]` maggiore o uguale a 5000 diventa di colore verde limone. I valori di `[Sum(Sales)]` compresi tra 2500 e 5000 vengono visualizzati in giallo, mentre quelli minori di 2500 in rosso.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nella riga del subtotale in cui sono visualizzate le vendite per una sottocategoria, il colore di sfondo della cella è rosso, giallo o verde a seconda del valore della somma delle vendite.  

![report-builder-kpi-colors](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4. Visualizzare un indicatore KPI tramite un misuratore  
Un misuratore raffigura un singolo valore di un set di dati. In questa esercitazione viene usato un misuratore lineare orizzontale poiché la relativa forma e semplicità ne rende facile la lettura anche quando è di piccole dimensioni e viene usato all'interno di una cella della tabella. Per altre informazioni, vedere [Misuratori &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando un misuratore  
  
1.  Passare alla visualizzazione della struttura.  
  
2.  Nella tabella fare clic con il pulsante destro del mouse sul quadratino della colonna Sales > **Inserisci colonna** > **a destra**. Alla tabella verrà aggiunta una nuova colonna.  

    ![report-builder-kpi-insert-column](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  Digitare **Linear KPI** nell'intestazione di colonna.  
  
4.  Nella scheda **Inserimento** > **Visualizzazioni dati** > **Misuratore** fare clic nell'area di progettazione esterna alla tabella.   
  
5.  Nella finestra di dialogo **Seleziona tipo di misuratore** selezionare il primo misuratore lineare **Orizzontale**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nell'area di progettazione verrà aggiunto un misuratore.  
  
7.  Dal riquadro Dati report trascinare il campo `Sales` nel misuratore. Viene visualizzato il riquadro **Dati del misuratore** .  
  
    Quando si rilascia il campo `Sales` nel misuratore, il campo viene aggiunto all'elenco **Valori** e viene aggregando usando la funzione SUM predefinita.  
   
    ![report-builder-kpi-drag-sales-field](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. Nel riquadro **Dati del misuratore** fare clic sulla freccia accanto a **LinearPointer1** > **Proprietà indicatore di misura**.  
  
10. Nella finestra di dialogo **Proprietà indicatore di misura lineare** > scheda **Opzioni dell'indicatore di misura** > **Tipo di indicatore di misura** assicurarsi che l'opzione**Barre** sia selezionata. 
 
11. Fare clic su **OK**.  
  
12. Fare clic con il pulsante destro del mouse sulla scala nel misuratore e selezionare **Proprietà scala**.  
  
13. Nella finestra di dialogo **Proprietà scala lineare**> scheda **Generale** impostare il valore **Massimo** su 25000.  

    > [!NOTE]  
    > Per calcolare dinamicamente il valore dell'opzione **Massimo** è possibile usare un'espressione invece di una costante, ad esempio 25000. L'espressione utilizzerebbe in tal caso l'aggregazione della funzionalità di aggregazione, rendendola simile all'espressione `=Max(Sum(Fields!Sales.value), "Tablix1")`.  

14. Nella scheda **Etichette** selezionare **Nascondi etichette scala**.

15. Fare clic su **OK**.
  
14. Trascinare il misuratore all'interno della tabella, nella seconda cella vuota della colonna Linear KPI, nella riga che visualizza le vendite del subtotale per il campo `Subcategory` , accanto al campo in cui è stata aggiunta la formula per il colore dello sfondo.  
  
    > [!NOTE]  
    > Potrebbe essere necessario ridimensionare la colonna in modo che il misuratore lineare orizzontale rientri nella cella. Per ridimensionare la colonna, selezionare la tabella e trascinare i quadratini della colonna. L'area di progettazione del report viene adattata per accogliere la tabella.  
  
15. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
    La lunghezza orizzontale della barra verde nel misuratore cambia in base al valore dell'indicatore KPI.  
  
![report-builder-linear-kpi](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5. Visualizzare un indicatore KPI tramite un indicatore  
Gli indicatori sono piccoli e semplici misuratori che consentono di visualizzare i valori dei dati in modo immediato. Grazie alle loro dimensioni e alla semplicità, gli indicatori vengono spesso utilizzati nelle tabelle e nelle matrici. Per altre informazioni, vedere [Indicatori &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Per visualizzare lo stato attuale di un indicatore KPI utilizzando un indicatore  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nella tabella fare clic con il pulsante destro del mouse sul quadratino della colonna Linear KPI aggiunta nell'ultima procedura > **Inserisci colonna**  > **a destra**. Alla tabella verrà aggiunta una nuova colonna.  
  
3.  Digitare **Stoplight KPI** nell'intestazione di colonna.  
  
4.  Selezionare la cella del subtotale della categoria accanto al misuratore lineare aggiunto nell'ultima procedura.  
  
5.  Nella scheda **Inserisci**> **Visualizzazioni dati** > fare doppio clic su **Indicatore**.  
  
6.  Nella finestra di dialogo **Seleziona tipo indicatore** in **Forme**selezionare il primo tipo di forma **"3 semafori (con bordo)"** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    L'indicatore viene aggiunto alla cella nella nuova colonna Stoplight KPI.  
  
8.  Fare clic con il pulsante destro del mouse sull'indicatore e scegliere **Proprietà indicatore**.  
  
9. Nella scheda **Valore e stati** nella casella **Valore** selezionare **[SUM (Sales)]** . Non modificare le opzioni.  
  
    Per impostazione predefinita, si verifica la sincronizzazione dei dati nell'area dati e il valore **Tablix1**, ovvero il nome dell'area dati della tabella nel report, viene visualizzato nella casella **Ambito sincronizzazione** .  
  
    In questo report, è possibile anche modificare l'ambito di un indicatore posizionato nella cella del subtotale della sottocategoria per eseguire la sincronizzazione nel campo SalesDate.  
  
11. Fare clic su **OK**.

11. Fare clic su **Esegui** per visualizzare l'anteprima del report.  

![report-builder-kpi-stoplight](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6. Aggiungere un titolo al report  
Nella parte superiore del report viene visualizzato il titolo del report. È possibile posizionare il titolo del report in un'apposita intestazione oppure, se ne è privo, in una casella di testo nella parte superiore del corpo del report. In questa sezione sarà usata la casella di testo che viene automaticamente posizionata nella parte superiore del corpo del report.  
  
Il testo può essere ulteriormente migliorato applicando stili di carattere, dimensioni e colori diversi alle frasi e ai singoli caratteri del testo. Per altre informazioni, vedere [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Product Sales KPIs**e fare clic all'esterno della casella di testo.  
  
3.  Facoltativamente, fare clic con il pulsante destro del mouse sulla casella di testo contenente **Product Sales KPI**, fare clic su **Proprietà casella di testo**. Nella scheda Carattere scegliere i diversi stili di carattere, dimensioni e colori.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="Save"></a>7. Salvare il report  
Salvare il report in un server di report o nel computer. Se il report non viene salvato nel server di report, non saranno disponibili alcune funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , ad esempio le parti del report e i sottoreport.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
    Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con **Product Sales KPI**.  
  
5.  Fare clic su **Salva**.  
  
Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**e selezionare la cartella in cui si vuole salvare il report.  
  
> [!NOTE]  
> Se non si ha accesso a un server di report, fare clic su **Desktop**, **Documenti**o **Risorse del computer** e salvare il report nel computer.  
  
1.  In **Nome**sostituire il nome predefinito con **Product Sales KPI**.  
  
2.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
Questo passaggio conclude l'esercitazione relativa all'aggiunta di un indicatore KPI al report. Per altre informazioni, vedere:
*  [Misuratori](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [Indicatori](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
* [Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md)
* [Generatore report in SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

