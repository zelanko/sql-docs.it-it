---
title: 'Esercitazione: Report mappa (Generatore report) | Microsoft Docs'
ms.date: 08/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4db47bde02745ddc554f17e1f951c836c1542cc8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63041575"
---
# <a name="tutorial-map-report-report-builder"></a>Esercitazione: Report mappa (Generatore report)
Questa esercitazione di [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] illustra le funzionalità della mappa che si possono usare per visualizzare i dati su uno sfondo geografico in un report impaginato di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . 
  
Le mappe sono basate su dati spaziali costituiti in genere da punti, linee e poligoni. Un poligono può ad esempio rappresentare la struttura di una regione, una riga può rappresentare una strada e un punto può rappresentare la posizione geografica di una città. Ogni tipo di dati spaziali viene visualizzato su un livello mappa separato come un set di elementi mappa.  
  
Per variare l'aspetto degli elementi mappa, è possibile specificare un campo contenente valori corrispondenti agli elementi mappa con dati analitici provenienti da un set di dati. È inoltre possibile definire regole per variare il colore, la dimensione o altre proprietà in base a intervalli di dati.  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
In questa esercitazione viene compilato un report mappa in cui sono visualizzate le posizioni di alcuni negozi nelle regioni dello stato di New York.  
   
> [!NOTE]  
> In questa esercitazione, i passaggi della procedura guidata sono consolidati in due procedure: una per la creazione del set di dati e un'altra per la creazione di una tabella. Per istruzioni dettagliate su come selezionare un server di report, scegliere un'origine dati, creare un set di dati ed eseguire la procedura guidata. Vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo stimato per il completamento dell'esercitazione: 30 minuti.  
  
## <a name="requirements"></a>Requisiti  
Per questa esercitazione è necessario configurare il server di report affinché supporti le mappe Bing come sfondo. Per altre informazioni, vedere [Pianificare il supporto dei report mappa](https://msdn.microsoft.com/5ddc97a7-7ee5-475d-bc49-3b814dce7e19). 

Per informazioni su altri requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Map"></a>1. Creare una mappa con un livello poligono dalla Creazione guidata mappa  
In questa sezione si aggiunge una mappa al report dalla raccolta mappe. La mappa dispone di un livello in cui sono visualizzate le regioni dello stato di New York. La forma di ogni regione è data da un poligono basato su dati spaziali incorporati nella mappa dalla raccolta mappe.  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Per aggiungere una mappa con l'apposita creazione guidata in un nuovo report  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal computer, dal portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o in modalità integrata SharePoint.  
  
    Si apre la finestra di dialogo **Nuovo report o set di dati** .  
  
    Se la finestra di dialogo **Nuovo report o set di dati** non viene visualizzata, scegliere **Nuovo** dal menu **File**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata mappa**.  
  
4.  Nella pagina **Scegliere un'origine dati spaziali** , verificare che sia selezionata l'opzione **Raccolta mappe** .  
  
6.  Nel riquadro Raccolta mappe espandere **States by County** sotto **USA**, quindi fare clic su **New York**.  
  
    Nel riquadro Anteprima mappe viene visualizzata la mappa della regione di New York.  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina **Scegli opzioni di dati spaziali e vista mappa** accettare le impostazioni predefinite e fare clic su **Avanti**. 
 
    Per impostazione predefinita, gli elementi della mappa di una raccolta mappe vengono incorporati automaticamente nella definizione del report.  
  
9. Nella pagina **Scegli vista mappa** verificare che sia selezionata l'opzione **Mappa di base** e fare clic su **Avanti**.  
  
11. Nella pagina **Scegliere combinazione di colori e visualizzazione dati** selezionare l'opzione **Visualizza etichette** .  
  
12. Se è selezionata, deselezionare l'opzione **Mappa a colore singolo** .  
  
13. Nell'elenco a discesa **Campo dati** fare clic su **#COUNTYNAME**. Nel riquadro Anteprima mappe della procedura guidata vengono visualizzati gli elementi seguenti:  
  
    -   Un titolo con il testo **Titolo mappa**.  
  
    -   Una mappa in cui sono visualizzate le regioni di New York, ognuna con un colore diverso, con il relativo nome visualizzato nella posizione più adatta sull'area della regione.  
  
    -   Una legenda che contiene un titolo e un elenco di elementi da 1 a 5.  
  
    -   Una scala dei colori che contiene valori da 0 a 160 e nessun colore.  
  
    -   Una scala distanza in cui sono visualizzati chilometri (km) e miglia (mi).  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. Fare clic su **Fine**.  
  
    La mappa viene aggiunta all'area di progettazione.  
  
13. Selezionare il testo "Map Title" e il tipo **Sales by Store** > INVIO.  

15. Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa**. Nel riquadro **Livelli mappa** viene visualizzato un livello poligono, PolygonLayer1, di tipo **Incorporato**. Ogni regione è un elemento incorporato della mappa a questo livello.  
  
    > [!NOTE]  
    > Se il riquadro **Livelli mappa** non è visibile, è possibile che sia visualizzato all'esterno della vista corrente. Utilizzare la barra di scorrimento nella parte inferiore della visualizzazione della struttura per modificare la visualizzazione. In alternativa, nella scheda **Visualizza** , deselezionare l'opzione **Dati report** per ampliare l'area di progettazione.   

15. Selezionare la freccia accanto a PolygonLayer1 > **Proprietà poligono**.

16. Nella scheda **Carattere** modificare il colore in **Grigio tenue**.

17. Nella scheda **Home** fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
Nel report visualizzabile è incluso il titolo della mappa, la mappa e la scala distanza. Le regioni si trovano su un livello poligono della mappa. Ogni regione è data da un poligono che varia in base ai colori di una tavolozza, tuttavia i colori non sono associati ad alcun dato. Nella scala distanza sono visualizzate le distanze sia in chilometri sia in miglia.  
  
La legenda della mappa e la scala dei colori non sono ancora visibili perché alle regioni non sono associati dati analitici. I dati analitici verranno aggiunti in seguito in questa esercitazione.  
  
## <a name="PointLayer"></a>2. Aggiungere un livello punto mappa per visualizzare le posizioni dei negozi  
In questa sezione viene usata la Creazione guidata livello mappa per aggiungere un livello punto in cui vengono visualizzate le posizioni dei negozi.  
  
> [!NOTE]  
> In questa esercitazione la query contiene i valori dei dati e non richiede un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Per aggiungere un livello punto in base a una query spaziale di SQL Server  
  
1.  Nella scheda **Esegui** fare clic su > **Progettazione** per tornare alla visualizzazione Progettazione.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livelli mappa** . Sulla barra degli strumenti fare clic sul pulsante **Creazione guidata nuovo livello** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"). 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  Nella pagina **Scegliere un'origine dati spaziali** selezionare **Query spaziale di SQL Server**e fare clic su **Avanti**.  
  
4.  Nella pagina **Scegliere un set di dati con dati spaziali di SQL Server** fare clic su **Aggiungere un nuovo set di dati con dati spaziali di SQL Server** > **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati spaziali di SQL Server** selezionare un'origine dati esistente o il server di report, quindi selezionare un'origine dati.  

    > [!NOTE]  
    > L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Fare clic su **Avanti**.  
  
7.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
8.  Copiare il testo seguente e incollarlo nel riquadro della query:  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. Nella barra degli strumenti Progettazione query fare clic su **Esegui** ( **!** ).  
  
    Il set di risultati contiene sette colonne che rappresentano un gruppo di punti vendita nello stato di New York che vendono beni di consumo. Di seguito è riportato un elenco, con le spiegazioni per gli elementi che possono non essere evidenti: 
    *   **StoreKey**: identificatore di un negozio.  
    *   **StoreName**.
    *   **SellingArea**: l'area disponibile per la visualizzazione dei prodotti, che va da circa 42 metri quadrati a circa 104 metri quadrati.
    *   **City**.
    *   **County**.
    *   **Vendite**: vendite totali. 
    *   **SpatialLocation**: percorso in longitudine e latitudine. 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. Fare clic su **Avanti**.  
  
    Il set di dati del report denominato DataSet1 viene creato automaticamente. Al termine della procedura guidata, è possibile visualizzare la relativa raccolta campi nel riquadro Dati report.  
  
11. Nella pagina **Scegli opzioni di dati spaziali e vista mappa** verificare che **Campo spaziale** sia impostato su **SpatialLocation** e che **Tipo livello** sia impostato su **Punto**. Accettare le altre impostazioni predefinite di questa pagina.  
  
    Nella vista mappa vengono visualizzati cerchi che indicano la posizione di ogni negozio.  
  
12. Fare clic su **Avanti**.  
  
13. Nella pagina Scegli vista mappa fare clic su **Mappa a bolle** per un tipo di mappa che visualizza marcatori le cui dimensioni variano in base ai dati. Fare clic su **Avanti**.  
  
14. Nella pagina **Scegli il set di dati analitici** fare clic su DataSet1 e quindi su **Avanti**. Questo set di dati contiene sia dati analitici sia dati spaziali che verranno visualizzati al nuovo livello punto.   
  
16. Nella pagina **Scegliere combinazione di colori e visualizzazione dati** selezionare **Usa dimensioni bolla per visualizzare i dati**.  
  
17. In **Campo dati**selezionare `[Sum(SellingArea)]` per variare i tipi di marcatore in base alle dimensioni dell'area che un negozio ha riservato all'esposizione dei prodotti.  
  
18. Selezionare **Visualizza etichette**e in **Campo dati**selezionare `[City]`.

18. Fare clic su **Fine**.  
  
    Il livello mappa viene aggiunto al report. Nella legenda vengono visualizzate le dimensioni bolla in base ai valori indicati in SellingArea.  
  
 19. Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Nel riquadro **Livello mappa** viene visualizzato un nuovo livello, PointLayer1, con il tipo di origine dati spaziali **DataRegion**.  
  
19. Aggiungere un titolo della legenda. Nella legenda selezionare il testo **Titolo**, digitare **Display Area (sq. ft.)** e premere INVIO.  
  
21. Nel riquadro **Livelli mappa**fare clic sulla freccia accanto a PointLayer1 e quindi fare clic su **Proprietà punto**.  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. Nella scheda **Carattere** impostare lo stile su **Grassetto** e le dimensioni su **10pt**.

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. Nella scheda **Generale** selezionare **In basso** per **Posizione**.

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Fare clic su **Esegui** per visualizzare l'anteprima del report.  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    Sulla mappa vengono visualizzate le posizioni dei negozi nello Stato di New York. La dimensione del marcatore per ogni negozio è basata sull'area di visualizzazione. Cinque intervalli dell'area di visualizzazione sono stati calcolati automaticamente.


  
## <a name="LineLayer"></a>3. Aggiungere un livello linea mappa per visualizzare un itinerario  
Utilizzare la Creazione guidata livello mappa per aggiungere un livello mappa in cui venga visualizzata un itinerario tra due negozi. In questa esercitazione il percorso viene creato da tre posizioni di negozi. In un'applicazione aziendale il percorso potrebbe essere l'itinerario migliore tra negozi.  
  
### <a name="to-add-a-line-layer-to-map"></a>Per aggiungere un livello linea a una mappa  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti fare clic sul pulsante **Creazione guidata nuovo livello** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  Nella pagina **Scegliere un'origine dati spaziali** selezionare **Query spaziale di SQL Server** e fare clic su **Avanti**.  
  
4.  Nella pagina **Scegliere un set di dati con dati spaziali di SQL Server** fare clic su **Aggiungere un nuovo set di dati con dati spaziali di SQL Server** , quindi su **Avanti**.  
  
5.  In **Scegliere una connessione a un'origine dati spaziali di SQL Server**selezionare DataSource1, l'origine dati usata durante la prima procedura.  
  
6.  Fare clic su **Avanti**.  
  
7.  Nella pagina **Progetta query** fare clic su **Modifica come testo**. Progettazione query passa alla modalità basata su testo.  
  
8.  Incollare il testo seguente nel riquadro della query:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Fare clic su **Avanti**.  
  
    Sulla mappa viene visualizzato un percorso tra tre negozi.  
  
10. Nella pagina **Scegli opzioni di dati spaziali e vista mappa** verificare che **Campo spaziale** sia impostato su **Route** e che **Tipo livello** sia impostato su **Linea**. Accettare le altre impostazioni predefinite.  
  
    Nella vista mappa viene visualizzato un percorso da un negozio nella parte nord dello stato di New York a un negozio nella parte sud dello stesso stato.  
  
11. Fare clic su **Avanti**.  
  
12. Nella pagina **Scegli vista mappa** fare clic su **Mappa linea di base**e quindi su **Avanti**.  
  
13. In **Scegliere combinazioni di colori e visualizzazione dati**selezionare l'opzione **Mappa a colore singolo**. Il percorso viene visualizzato in un determinato colore che dipende dal tema selezionato.  
  
14. Fare clic su **Fine**.  

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     Nella mappa viene visualizzato un nuovo livello linea con un'origine dati spaziali di tipo **DataRegion**. In questo esempio i dati spaziali provengono da un set di dati, tuttavia nessun dato analitico è associato alla riga.  

## <a name="adjust-the-zoom"></a>Regolare lo zoom
1. Se non è possibile visualizzare l'intero stato di New York, si può regolare lo zoom. Con la mappa selezionata, nel riquadro Proprietà vengono visualizzate le proprietà **MapViewport** . 

15. Espandere la sezione **Visualizzazione** , quindi espandere **Visualizzazione** in modo da visualizzare la proprietà **Zoom** . Impostarla su **125**. 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      Questa è la percentuale di zoom. Al 125% verrà visualizzato l'intero stato.
  
## <a name="TileLayer"></a>4. Aggiungere uno sfondo a tessere mappa di Bing  
In questa sezione si aggiunge un livello mappa in cui viene visualizzato uno sfondo a tessere mappa di Bing.  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti fare clic su **Aggiungi livello** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  Nell'elenco a discesa fare clic su **Livello sezione**.  
  
    L'ultimo livello nel riquadro **Livello mappa** è TileLayer1. Per impostazione predefinita, il livello sezione visualizza lo stile della mappa stradale.  
  
    > [!NOTE]  
    > Nella procedura guidata è anche possibile aggiungere un livello sezione nella pagina **Scegli opzioni di dati spaziali e vista mappa** . A tale scopo, selezionare **Aggiungi sfondo Bing Maps per la vista mappa**. In un report visualizzabile, lo sfondo a sezioni visualizza le tessere mappa di Bing per l'attuale livello di allineamento al centro e zoom del viewport mappa.  
  
4.  Fare clic sulla freccia accanto a TileLayer1 > **Proprietà sezione**.  
  
5.  Nella scheda **Generale** selezionare **Aereo**per **Tipo**. La vista aerea non contiene testo.  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="Transparent"></a>5. Rendere trasparente un livello  
Questa sezione spiega come rendere visibili gli elementi su un livello attraverso un altro livello, regolando l'ordine e la trasparenza dei livelli fino a ottenere l'effetto desiderato. Si inizia con il primo livello creato, PolygonLayer1. 
  
1.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
3.  Fare clic sulla freccia accanto a PolygonLayer1 > **Dati livello**. Viene visualizzata la finestra di dialogo **Proprietà livello poligono mappa** .  
  
4.  Nella scheda **Visibilità** digitare **30**per **Trasparenza (percentuale)** .  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     L'area di progettazione visualizza le regioni in modo semitrasparente.  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="Vary"></a>6. Variare il colore delle regioni in base alle vendite  
Ogni regione del livello poligono dispone di un colore diverso perché l'elaboratore di report assegna automaticamente un valore di colore dall'apposita tavolozza in base al tema scelto nell'ultima pagina della creazione guidata mappa.  
  
In questa sezione si specifica una regola colore per associare colori specifici a un intervallo di vendite di negozi per ogni regione. I colori rosso-giallo-verde indicano vendite elevate-medie-basse. Formattare la scala dei colori per mostrare la valuta. Visualizzare gli intervalli di vendite annuali in una nuova legenda. Per le regioni in cui non sono presenti negozi, non utilizzare alcun colore per mostrare che non ci sono dati associati.  
  
### <a name="Relationship"></a>6a. Compilare una relazione tra dati spaziali e dati analitici  
Per variare le forme delle regioni per colore in base ai dati analitici, è necessario per prima cosa associare i dati analitici a quelli spaziali. In questa esercitazione verrà utilizzato il nome della regione su cui basare la corrispondenza. 
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livelli mappa** .  
  
3.  Fare clic sulla freccia accanto a PolygonLayer1 &gt;, quindi su **Dati livello**. Viene visualizzata la finestra di dialogo **Proprietà livello poligono mappa** .  
  
4.  Nella scheda **Dati analitici** selezionare DataSet1 in **Set di dati analitici**. Questo set di dati è stato creato dalla procedura guidata quando è stata creata la query dei dati spaziali per le regioni.  
  
6.  In **Campi per corrispondenze**fare clic su **Aggiungi**. Viene aggiunta una nuova riga.  
  
7.  In **Da set di dati spaziale**fare clic su COUNTYNAME.  
  
8.  In **Da set di dati analitico**fare clic su COUNTYNAME.  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Visualizzare l'anteprima del report.  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
Specificando un campo delle corrispondenze dall'origine dati spaziali e dal set di dati analitico, si consente all'elaboratore di report di raggruppare i dati analitici in base agli elementi della mappa. Un elemento della mappa associato a dati presenta una corrispondenza corretta per i valori specificati.  
  
Ogni regione che contiene un negozio è caratterizzata da un colore basato sulla tavolozza dei colori per lo stile scelto nella procedura guidata. Le altre regioni vengono visualizzate in grigio.  
  
### <a name="ColorRules"></a>6b. Specificare le regole colori per i poligoni  
Per creare una regola per variare il colore di ogni regione in base alle vendite dei negozi, è necessario specificare i valori di intervallo, il numero di divisioni all'interno dell'intervallo che si desidera visualizzare e i colori da utilizzare.  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Per specificare le regole colori per tutti i poligoni a cui sono associati dati  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic sulla freccia accanto a PolygonLayer1, quindi su **Regola colore poligono**. Viene visualizzata la finestra di dialogo **Proprietà regole colori mappa** . Si noti che l'opzione della regola colore **Visualizza dati tramite tavolozza colori** è selezionata. Questa opzione è stata impostata dalla procedura guidata.  
  
3.  Selezionare **Visualizza dati tramite intervalli colori**. L'opzione della tavolozza viene sostituita dalle opzioni colore iniziale, colore intermedio e colore finale.  
  
4.  Definire i valori di intervallo per le vendite per regione. In **Campo dati**selezionare `[Sum(Sales)]`nell'elenco a discesa.  
  
5.  Per modificare il formato per visualizzare la valuta in migliaia, modificare l'espressione nel modo seguente: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Impostare **Colore iniziale** su **Rosso**.  
  
7.  Impostare **Colore finale** su **Verde**.  
  
    **Rosso** rappresenta valori di vendite bassi, **Giallo** rappresenta valori di vendite medi e **Verde** rappresenta valori di vendite elevati. L'elaboratore di report calcola un intervallo di colori in base a questi valori e alle opzioni scelte nella pagina **Distribuzione** .  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  Fare clic su **Distribuzione**.  
  
9. Verificare che il tipo di distribuzione sia **Ottimale**. Per l'espressione del passaggio 5, la distribuzione ottimale divide i valori in base a intervalli secondari che bilanciano il numero di elementi e l'estensione di ogni intervallo.  
  
10. Accettare i valori predefiniti per le altre opzioni di questa pagina. Quando si seleziona il tipo di distribuzione ottimale, il numero di intervalli secondari viene calcolato durante l'esecuzione del report.  
  
11. Fare clic su **Legenda**.  
  
12. In **Opzioni scala dei colori**verificare che l'opzione **Mostra nella scala dei colori** sia selezionata.  
  
13. In **Mostra in questa legenda**selezionare la riga vuota nell'elenco a discesa. Per il momento, gli intervalli di colore saranno visualizzati solo nella scala dei colori.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. Visualizzare l'anteprima del report.

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    La scala dei colori visualizza quattro colori: rosso, arancione, giallo e verde. Ogni colore rappresenta un intervallo di vendite che viene calcolato automaticamente in base alle vendite di ogni regione.  
  
### <a name="ColorScale"></a>6c. Formattare i dati nella scala dei colori come valuta  
Per impostazione predefinita, i dati presentano un formato generale. In questa sezione, vengono applicati i formati personalizzati.  
  
1. Passare alla Visualizzazione della struttura.  

2. Selezionare la scala dei colori. Nella sezione **Numero** della scheda **Home** fare clic su **Valuta**.  
  
4.  Sempre nella sezione **Numero** fare clic due volte sul pulsante **Diminuisci decimali** .  
  
    La scala dei colori visualizza le vendite annuali nel formato della valuta per ogni intervallo.  
  
### <a name="NewLegend"></a>6d. Aggiungere un titolo della legenda   
  
1.  Con la scala dei colori ancora selezionata, nel riquadro Proprietà vengono visualizzate le proprietà per **MapColorScale**. 
  
2. Espandere la sezione del titolo e nella proprietà Caption digitare **Sales (Thousands)** .

3. Modificare la proprietà TextColor in **Bianco**.  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  Visualizzare l'anteprima del report.  
  
Le regioni a cui sono associati negozi e vendite vengono visualizzate in base alle regole colori. Le regioni a cui non sono associate vendite non presentano colori.  
  
### <a name="NoData"></a>6f. Modificare il colore per le regioni prive di dati  
È possibile impostare le opzioni di visualizzazione predefinite per tutti gli elementi della mappa su un livello. Le regole colori hanno la precedenza su queste opzioni di visualizzazione.  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Per impostare le proprietà di visualizzazione per tutti gli elementi su un livello  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
3.  Fare clic sulla freccia giù per PolygonLayer1, quindi su **Proprietà poligono**. 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     Viene visualizzata la finestra di dialogo **Proprietà poligono mappa** . Le opzioni di visualizzazione impostate in questa finestra di dialogo sono applicabili a tutti i poligoni del livello prima che vengano applicate le opzioni di visualizzazione basate su regola.  
  
4.  Nella scheda **Riempimento** verificare che lo stile di riempimento sia **Tinta unita**. Le sfumature e i modelli si applicano a tutti i colori.  
  
6.  In **Colore**selezionare **Acciaio chiaro**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualizzare l'anteprima del report.  
  
Le regioni a cui non sono associati dati vengono visualizzate in grigio-blu. Solo per le regioni a cui sono associati dati analitici vengono usati i colori da **Rosso** a **Verde** secondo le regole colori specificate.  
  
## <a name="CustomPoint"></a>7. Aggiungere un punto personalizzato  
Per rappresentare un nuovo negozio che non è ancora stato creato, specificare un punto e usare il tipo di marcatore **Stella** .  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti fare clic su **Aggiungi livello** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer"), quindi fare clic su **Livello punto**.  
  
    Un nuovo livello punto viene aggiunto alla mappa. Per impostazione predefinita, il livello punto usa il tipo di dati spaziali **Incorporato**.  
  
3.  Fare clic sulla freccia in PointLayer2 > **Aggiungi punto**.  
  
4.  Spostare il puntatore sul viewport mappa. Il cursore passa alla selezione di precisione.  
  
5.  Fare clic sulla posizione sulla mappa in cui si desidera aggiungere un punto. In questa esercitazione, fare clic su una posizione nella regione di Oneida. Un punto contrassegnato da un cerchio viene aggiunto al livello nella posizione selezionata. Per impostazione predefinita, il punto viene selezionato.  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  Fare clic con il pulsante destro del mouse sul punto aggiunto, quindi scegliere **Proprietà punto incorporato**.  
  
7.  Selezionare **Ignora opzioni punto per questo livello**. Nella finestra di dialogo vengono visualizzate pagine aggiuntive. I valori impostati qui hanno la precedenza sulle opzioni di visualizzazione per il livello o per le regole colori.  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  Nella scheda **Marcatore** selezionare **Stella**per **Tipo di marcatore**.  

10. Impostare **Dimensioni marcatore** su **18pt**.
  
3.  Nella scheda **Etichette** digitare **Nuovo negozio**in **Testo etichetta**.  
  
5.  In **Posizione**fare clic su **Torna all'inizio**.  

13. Nella scheda **Carattere** impostare la dimensione su **10pt** e lo stile su **Grassetto**.

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualizzare l'anteprima del report.  
  
L'etichetta viene visualizzata sopra la posizione del negozio.  

![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="CenterView"></a>8. Centrare e ridimensionare la mappa   
Questa sezione illustra come modificare il centro della mappa e un modo alternativo per modificare il livello di zoom.  
 
1.  Passare alla Visualizzazione della struttura.  

1.  Selezionare la mappa, quindi fare clic con il pulsante destro del mouse e scegliere **Proprietà viewport**.  
  
2.  Nella scheda **Allineamento al centro e zoom** verificare che sia selezionata l'opzione **Imposta un livello di allineamento al centro e zoom della vista** .  

4. Impostare **Livello zoom (percentuale)** su **125**.
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare clic sulla mappa e trascinarla in modo da posizionarla al centro.  
  
6.  Usare la rotella del mouse per modificare il livello di zoom.  
  
7.  Visualizzare l'anteprima del report.  
  
Nella visualizzazione della struttura la mappa nell'area di visualizzazione e la visualizzazione sono basate su dati di esempio. Nel report visualizzabile, la vista mappa è allineata al centro della vista specificata.  
  
## <a name="Title"></a>9. Aggiungere un titolo al report  
  
1.  Passare alla Visualizzazione della struttura.
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite nei punti vendita di New York** , quindi fare clic all'esterno della casella di testo.  
  
Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
## <a name="Save"></a>10. Salvare il report  
  
1.  Nella visualizzazione Progettazione o Anteprima fare clic sul menu **File** > **Salva con nome**.
 
3.  In **Nome**digitare **Punti vendita di New York - vendite**.  

3. Salvare il documento nel computer locale o in un server [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .
  
4. Fare clic su **Salva**. 

Se si salva in un server di report, è possibile visualizzarlo su tale server.

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>Passaggi successivi  
Questa operazione conclude la procedura dettagliata per l'aggiunta di una mappa al report.  
  
Per altre informazioni, vedere [Mappe &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
[Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md)  
[Generatore report in SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  

