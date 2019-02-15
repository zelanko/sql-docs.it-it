---
title: 'Esercitazione: Report mappa (Generatore Report) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5522f24dbb7b930b69b2656f7c2c5b53954f16ca
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290919"
---
# <a name="tutorial-map-report-report-builder"></a>Esercitazione: Report mappa (Generatore report)
  Questa esercitazione intende fornire un approfondimento delle funzionalità della mappa che è possibile utilizzare per visualizzare i dati del report rispetto a uno sfondo geografico.  
  
 Le mappe sono basate su dati spaziali costituiti in genere da punti, linee e poligoni. Un poligono può ad esempio rappresentare la struttura di una regione, una riga può rappresentare una strada e un punto può rappresentare la posizione geografica di una città. Ogni tipo di dati spaziali viene visualizzato su un livello mappa separato come un set di elementi mappa.  
  
 Per variare l'aspetto degli elementi mappa, è possibile specificare un campo contenente valori corrispondenti agli elementi mappa con dati analitici provenienti da un set di dati. È inoltre possibile definire regole per variare il colore, la dimensione o altre proprietà in base a intervalli di dati.  
  
 In questa esercitazione verrà compilato un report mappa in cui sono visualizzate le posizioni di alcuni negozi nelle regioni dello stato di New York.  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
1.  [Creare una mappa con un livello poligono dalla creazione guidata mappa](#Map)  
  
2.  [Aggiungere un livello punto mappa ai percorsi di visualizzazione Store](#PointLayer)  
  
3.  [Aggiungere un livello linea mappa per visualizzare un itinerario](#LineLayer)  
  
4.  [Aggiungere un sfondo a tessere mappe Bing](#TileLayer)  
  
5.  [Rendere trasparente un livello](#Transparent)  
  
6.  [Variare colore delle regioni in base alle vendite](#Vary)  
  
    1.  [Compilare una relazione tra dati spaziali e analitici](#Relationship)  
  
    2.  [Specificare le regole colore per poligoni](#ColorRules)  
  
    3.  [Formattare i dati nella scala dei colori come valuta](#ColorScale)  
  
    4.  [Creare una nuova legenda](#NewLegend)  
  
    5.  [Associare la legenda e le regole colore](#Associate)  
  
    6.  [Cancellare il colore dalle regioni senza dati](#NoData)  
  
7.  [Aggiungere un punto personalizzato](#CustomPoint)  
  
8.  [Allineare al centro la vista mappa](#CenterView)  
  
9. [Aggiungere un titolo al Report](#Title)  
  
10. [Salvare il Report](#Save)  
  
> [!NOTE]  
>  In questa esercitazione, i passaggi della procedura guidata sono consolidati in due procedure: una per la creazione del set di dati e un'altra per la creazione di una tabella. Per istruzioni dettagliate su come selezionare un server di report, scegliere un'origine dati, creare un set di dati ed eseguire la procedura guidata, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un Report tabella semplice &#40;Generatore Report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tempo previsto per il completamento di questa esercitazione: 30 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Map"></a> 1. Creare una mappa con un livello poligono dalla Creazione guidata mappa  
 Aggiungere una mappa al report dalla raccolta mappe. La mappa dispone di un livello in cui sono visualizzate le regioni dello stato di New York. La forma di ogni regione è data da un poligono basato su dati spaziali incorporati nella mappa dalla raccolta mappe.  
  
#### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Per aggiungere una mappa con l'apposita creazione guidata in un nuovo report  
  
1.  Fare clic su **avviare**, scegliere **programmi**, scegliere [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **Generatore Report**, quindi fare clic su **Generatore Report**.  
  
     Verrà visualizzata la finestra di dialogo Riquadro attività iniziale.  
  
    > [!NOTE]  
    >  Se la finestra di dialogo riquadro attività iniziale non viene visualizzato, dal pulsante Generatore Report, fare clic su **New**.  
  
2.  Nel riquadro sinistro, verificare che **Report** sia selezionata.  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata mappa**.  
  
4.  Fare clic su **Crea**.  
  
5.  **Scegliere un'origine dati spaziali** pagina, verificare che **raccolta mappe** sia selezionata.  
  
6.  Nel riquadro raccolta mappe, espandere **States by County** sotto **Stati Uniti**, fare clic su **New York**.  
  
     Nel riquadro Anteprima mappe viene visualizzata la mappa della regione di New York.  
  
7.  Scegliere **Avanti**.  
  
8.  Nel **scegliere i dati spaziali e Vista mappa opzioni** pagina, accettare le impostazioni predefinite. Per impostazione predefinita, gli elementi mappa di una raccolta mappe verranno incorporati automaticamente nella definizione del report.  
  
9. Scegliere **Avanti**.  
  
10. Nella pagina **Scegli vista mappa** verificare che sia selezionata l'opzione **Mappa di base** e fare clic su **Avanti**.  
  
11. Nella pagina **Scegliere combinazione di colori e visualizzazione dati** selezionare l'opzione **Visualizza etichette** .  
  
12. Se è selezionata, deselezionare l'opzione **Mappa a colore singolo** .  
  
13. Dal **datové** elenco a discesa fare clic su #COUNTYNAME. Nel riquadro Anteprima mappe della procedura guidata vengono visualizzati gli elementi seguenti:  
  
    -   Un titolo con il testo **Titolo mappa**.  
  
    -   Una mappa in cui sono visualizzate le regioni di New York, ognuna con un colore diverso, con il relativo nome visualizzato nella posizione più adatta sull'area della regione.  
  
    -   Una legenda che contiene un titolo e un elenco di elementi da 1 a 5.  
  
    -   Una scala dei colori che contiene valori da 0 a 160 e nessun colore.  
  
    -   Una scala distanza in cui sono visualizzati chilometri (km) e miglia (mi).  
  
14. Scegliere **Fine**.  
  
     La mappa viene aggiunta all'area di progettazione.  
  
15. Fare clic sulla mappa per selezionarla e visualizzare il **nel riquadro livelli mappa**. Il **nel riquadro livelli mappa** Mostra un livello poligono di tipo **Embedded**. Ogni regione è un elemento incorporato della mappa a questo livello.  
  
    > [!NOTE]  
    >  Se non viene visualizzato il **livelli mappa** riquadro potrebbero essere visualizzato all'esterno della vista corrente. Utilizzare la barra di scorrimento nella parte inferiore della visualizzazione della struttura per modificare la visualizzazione. In alternativa, nella **vista** scheda, deseleziona il **proprietà** o la **i dati del Report** opzione per fornire più aree di superficie di progettazione.  
  
16. Fare clic sul titolo della mappa e quindi fare clic su **proprietà titolo**.  
  
17. Sostituire il testo del titolo con **Sales by Store**.  
  
18. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
19. Visualizzare l'anteprima del report.  
  
 Nel report visualizzabile è incluso il titolo della mappa, la mappa e la scala distanza. Le regioni si trovano su un livello poligono della mappa. Ogni regione è data da un poligono che varia in base ai colori di una tavolozza, tuttavia i colori non sono associati ad alcun dato. Nella scala distanza sono visualizzate le distanze sia in chilometri sia in miglia.  
  
 La legenda della mappa e la scala dei colori non sono ancora visibili perché alle regioni non sono associati dati analitici. I dati analitici verranno aggiunti in seguito in questa esercitazione.  
  
##  <a name="PointLayer"></a> 2. Aggiungere un livello punto mappa per visualizzare le posizioni dei negozi  
 Utilizzare la Creazione guidata livello mappa per aggiungere un livello punto in cui vengono visualizzate le posizioni dei negozi.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Per aggiungere un livello punto in base a una query spaziale di SQL Server  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti, fare clic sul pulsante **Creazione guidata nuovo livello** ![rs_IconMapLayerWizard](../../2014/tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  Nella pagina **Scegliere un'origine dati spaziali** selezionare **Query spaziale di SQL Server**e fare clic su **Avanti**.  
  
4.  Nel **scegliere un set di dati con dati spaziali di SQL Server** pagina, fare clic su **aggiungere un nuovo set di dati con dati spaziali di SQL Server**e quindi fare clic su **Next**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati spaziali di SQL Server** selezionare un'origine dati esistente o il server di report, quindi selezionare un'origine dati.  
  
6.  Scegliere **Avanti**.  
  
7.  La progettazione di una pagina di Query, fare clic su **modifica come testo**.  
  
8.  Incollare il testo seguente nel riquadro della query:  
  
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
    UNION ALL Select 124 as StoreKey, 'Contoso Rochester No.2 Store' as StoreName, 700 as SellingArea, 'Rochester' as City, 'Monroe' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-77.6240415667866 43.1547066024338)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. Nella barra degli strumenti Progettazione query fare clic su **Esegui** (**!**).  
  
     Il set di risultati vengono visualizzate sette colonne: StoreKey, StoreName, SellingArea, City, County, Sales e SpatialLocation. Questi dati rappresentano un set di punti vendita nello Stato di New York che vendono beni di consumo. Ogni riga del set di risultati contiene un identificatore del negozio, il nome del negozio, l'area disponibile per l'esposizione dei prodotti, la città e la regione in cui si trova il negozio, il totale vendite e la posizione indicata con longitudine e latitudine. L'area di visualizzazione varia da 455 piedi quadrati a 1125 piedi quadrati.  
  
10. Scegliere **Avanti**.  
  
     Il set di dati del report denominato DataSet1 viene creato automaticamente. Al termine della procedura guidata, è possibile utilizzare Dati report per visualizzare la relativa raccolta campi.  
  
11. Nel **scegliere i dati spaziali opzioni e Vista mappa** verificare che il **campo spaziale** viene `SpatialLocation` e che il **tipo livello** è **punto**. Accettare le altre impostazioni predefinite di questa pagina.  
  
     Nella vista mappa vengono visualizzati cerchi che indicano la posizione di ogni negozio.  
  
12. Scegliere **Avanti**.  
  
13. Specificare un tipo di mappa in cui vengono visualizzati marcatori che variano in base ai dati analitici. La pagina Scegli Vista mappa, scegliere **mappa con marcatori analitici**, quindi fare clic su **successivo**.  
  
14. Nel **scegliere il set di dati analitici** fare clic su DataSet1. Questo set di dati contiene sia dati analitici sia dati spaziali che verranno visualizzati al nuovo livello punto.  
  
15. Scegliere **Avanti**.  
  
16. Nel **scegliere i colori del tema e visualizzazione dati** pagina, deseleziona le **Usa colori marcatore per visualizzare i dati** opzione e quindi selezionare l'opzione **Usa tipi marcatore per visualizzare i dati**.  
  
17. Nelle **datové**, selezionare `[Sum(SellingArea)]` per variare i tipi di marcatore per la dimensione dell'area di un negozio ha riservato all'esposizione dei prodotti.  
  
18. Scegliere **Fine**.  
  
     Il livello mappa viene aggiunto al report. Nella legenda vengono visualizzati i tipi di marcatore in base ai valori indicati in SellingArea.  
  
     Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Nel riquadro **Livello mappa** viene visualizzato un nuovo livello, PointLayer1, con il tipo di origine dati spaziali **DataRegion**.  
  
19. Aggiungere un titolo della legenda. Fare clic sul titolo della legenda e quindi fare clic su **proprietà titolo legenda**.  
  
20. Eliminare il titolo e digitare **Display Area (Square Feet)**.  
  
21. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
22. Visualizzare i valori predefiniti impostati dalla procedura guidata. Nel **nel riquadro livelli mappa**, fare clic sul livello punto e quindi fare clic su **regola tipo marcatore**.  
  
     Nel **generale** scheda marcatori sono elencati nell'ordine in cui compaiono nella legenda. Nel **distribuzione** scheda, il numero di intervalli secondari è 5. Nel **legenda** scheda, il testo della legenda è impostato per visualizzare il valore iniziale e finale in ogni intervallo.  
  
23. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Visualizzare l'anteprima del report.  
  
 Sulla mappa vengono visualizzate le posizioni dei negozi nello Stato di New York. Il tipo di marcatore per ogni negozio è basato sull'area di visualizzazione. Cinque intervalli dell'area di visualizzazione sono stati calcolati automaticamente.  
  
##  <a name="LineLayer"></a> 3. Aggiungere un livello linea mappa per visualizzare un itinerario  
 Utilizzare la Creazione guidata livello mappa per aggiungere un livello mappa in cui venga visualizzata un itinerario tra due negozi. In questa esercitazione il percorso viene creato da tre posizioni di negozi. In un'applicazione aziendale il percorso potrebbe essere l'itinerario migliore tra negozi.  
  
#### <a name="to-add-a-line-layer-to-map"></a>Per aggiungere un livello linea a una mappa  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti, fare clic su **Creazione guidata nuovo livello**.  
  
3.  Nella pagina **Scegliere un'origine dati spaziali** selezionare **Query spaziale di SQL Server** e fare clic su **Avanti**.  
  
4.  Nella pagina **Scegliere un set di dati con dati spaziali di SQL Server** fare clic su **Aggiungere un nuovo set di dati con dati spaziali di SQL Server** , quindi su **Avanti**.  
  
5.  Nel **scegliere una connessione a un'origine dati spaziali di SQL Server**, selezionare DataSource1, l'origine dati creata nella prima procedura.  
  
6.  Scegliere **Avanti**.  
  
7.  Nella pagina **Progetta query** fare clic su **Modifica come testo**. Progettazione query passa alla modalità basata su testo.  
  
8.  Incollare il testo seguente nel riquadro della query:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Scegliere **Avanti**.  
  
     Sulla mappa viene visualizzato un percorso tra tre negozi.  
  
10. Nella pagina **Scegli opzioni di dati spaziali e vista mappa** verificare che **Campo spaziale** sia impostato su **Route** e che **Tipo livello** sia impostato su **Linea**. Accettare le altre impostazioni predefinite.  
  
     Nella vista mappa viene visualizzato un percorso da un negozio nella parte nord dello stato di New York a un negozio nella parte sud dello stesso stato.  
  
11. Scegliere **Avanti**.  
  
12. Nella pagina **Scegli vista mappa** fare clic su **Mappa linea di base**e quindi su **Avanti**.  
  
13. In **Scegliere combinazioni di colori e visualizzazione dati**selezionare l'opzione **Mappa a colore singolo**. Il percorso viene visualizzato in un determinato colore che dipende dal tema selezionato.  
  
14. Scegliere **Fine**.  
  
 La mappa viene visualizzato un nuovo livello di riga con il tipo di origine dati spaziali **set di dati**. In questo esempio i dati spaziali provengono da un set di dati, tuttavia nessun dato analitico è associato alla riga.  
  
##  <a name="TileLayer"></a> 4. Aggiungere uno sfondo a tessere mappa di Bing  
 Aggiungere un livello mappa in cui sia visualizzato uno sfondo a tessere mappa di Bing.  
  
#### <a name="to-add-a-virtual-earth-tile-background"></a>Per aggiungere uno sfondo a sezioni Virtual Earth  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti, fare clic su **Aggiungi livello**![rs_IconMapAddLayer](../../2014/tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  Nell'elenco a discesa fare clic su **Livello sezione**.  
  
     L'ultimo livello nel riquadro **Livello mappa** è TileLayer1. Per impostazione predefinita, il livello sezione visualizza lo stile della mappa stradale.  
  
    > [!NOTE]  
    >  Nella procedura guidata è anche possibile aggiungere un livello sezione nella pagina **Scegli opzioni di dati spaziali e vista mappa** . A tale scopo, selezionare **Aggiungi sfondo Bing Maps per la vista mappa**. In un report visualizzabile, lo sfondo a sezioni visualizza le tessere mappa di Bing per l'attuale livello di allineamento al centro e zoom del viewport mappa.  
  
4.  Fare clic sulla freccia in giù in TileLayer1 e quindi fare clic su **proprietà del riquadro**.  
  
5.  Nelle **tipo**, selezionare **aeree**. La vista aerea non contiene testo.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Transparent"></a> 5. Rendere trasparente un livello  
 Per rendere visibili gli elementi su un livello attraverso un altro, è possibile regolare l'ordine dei livelli e la trasparenza di ogni livello fino a ottenere l'effetto desiderato.  
  
#### <a name="to-set-the-transparency-of-a-layer"></a>Per impostare la trasparenza di un livello  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
3.  Fare clic sulla freccia in giù in PolygonLayer1 e quindi fare clic su **dati livello**. Viene visualizzata la finestra di dialogo **Proprietà livello poligono mappa** .  
  
4.  Fare clic su **Visibilità**.  
  
5.  Nelle **trasparenza (%)**, digitare **30**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 L'area di progettazione visualizza le regioni in modo semitrasparente.  
  
##  <a name="Vary"></a> 6. Variare il colore delle regioni in base alle vendite  
 Ogni regione del livello poligono dispone di un colore diverso perché l'elaboratore di report assegna automaticamente un valore di colore dall'apposita tavolozza in base al tema scelto nell'ultima pagina della creazione guidata mappa.  
  
 Nei passaggi seguenti specificare una regola colore per associare colori specifici a un intervallo di vendite di negozi per ogni regione. I colori rosso-giallo-verde indicano vendite elevate-medie-basse. Formattare la scala dei colori per mostrare la valuta. Visualizzare gli intervalli di vendite annuali in una nuova legenda. Per le regioni in cui non sono presenti negozi, non utilizzare alcun colore per mostrare che non ci sono dati associati.  
  
###  <a name="Relationship"></a> 6a. Compilare una relazione tra dati spaziali e dati analitici  
 Per variare le forme delle regioni per colore in base ai dati analitici, è innanzitutto necessario associare i dati analitici a quelli spaziali. In questa esercitazione verrà utilizzato il nome della regione su cui basare la corrispondenza.  
  
##### <a name="to-build-a-relationship-between-spatial-data-and-analytical-data"></a>Per compilare una relazione tra i dati spaziali e i dati analitici  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
3.  Fare clic sulla freccia in giù in PolygonLayer1 e quindi fare clic su **dati livello**. Viene visualizzata la finestra di dialogo **Proprietà livello poligono mappa** .  
  
4.  Fare clic su **Dati analitici**.  
  
5.  Nell'elenco a discesa selezionare DataSet1. Questo set di dati è stato creato dalla procedura guidata quando è stata specificata la query dei dati spaziali per le regioni.  
  
6.  Nelle **campi per corrispondenze**, fare clic su **Add**. Viene aggiunta una nuova riga.  
  
7.  Nelle **dal set di dati spaziale**, dall'elenco a discesa elenco, fare clic su COUNTYNAME.  
  
8.  Nelle **dal set di dati analitici**, dall'elenco a discesa elenco, fare clic su Countyname.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Visualizzare l'anteprima del report.  
  
 Specificando un campo delle corrispondenze dall'origine dati spaziali e dal set di dati analitico, si consente all'elaboratore di report di raggruppare i dati analitici in base agli elementi della mappa. Un elemento della mappa associato a dati presenta una corrispondenza corretta per i valori specificati.  
  
 Ogni regione che contiene un negozio è caratterizzata da un colore basato sulla tavolozza dei colori per lo stile scelto nella procedura guidata.  
  
###  <a name="ColorRules"></a> 6b. Specificare le regole colori per i poligoni  
 Per creare una regola per variare il colore di ogni regione in base alle vendite dei negozi, è necessario specificare i valori di intervallo, il numero di divisioni all'interno dell'intervallo che si desidera visualizzare e i colori da utilizzare.  
  
##### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Per specificare le regole colori per tutti i poligoni a cui sono associati dati  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic sulla freccia in giù in PolygonLayer1 e quindi fare clic su **regola colore poligono**. Viene visualizzata la finestra di dialogo **Proprietà regole colori mappa** . Si noti che l'opzione della regola colore **Visualizza dati tramite tavolozza colori** è selezionata. Questa opzione è stata impostata dalla procedura guidata.  
  
3.  Selezionare **Visualizza dati tramite intervalli colori**. L'opzione della tavolozza viene sostituita dalle opzioni colore iniziale, colore intermedio e colore finale.  
  
4.  Definire i valori di intervallo per le vendite per regione. In **Campo dati**selezionare `[Sum(Sales)]`nell'elenco a discesa.  
  
5.  Per modificare il formato per visualizzare la valuta in migliaia, modificare l'espressione nel modo seguente: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Impostare **Colore iniziale** su **Rosso**.  
  
7.  Impostare **Colore finale** su **Verde**.  
  
     **Rosso** rappresenta valori di vendite bassi, **Giallo** rappresenta valori di vendite medi e **Verde** rappresenta valori di vendite elevati. L'elaboratore di report calcola un intervallo di colori in base a questi valori e alle opzioni scelte nella pagina **Distribuzione** .  
  
8.  Fare clic su **Distribuzione**.  
  
9. Verificare che il tipo di distribuzione sia **Ottimale**. Per l'espressione del passaggio 5, la distribuzione ottimale divide i valori in base a intervalli secondari che bilanciano il numero di elementi e l'estensione di ogni intervallo.  
  
10. Accettare i valori predefiniti per le altre opzioni di questa pagina. Quando si seleziona il tipo di distribuzione ottimale, il numero di intervalli secondari viene calcolato durante l'esecuzione del report.  
  
11. Fare clic su **Legenda**.  
  
12. In **Opzioni scala dei colori**verificare che l'opzione **Mostra nella scala dei colori** sia selezionata.  
  
13. In **Mostra in questa legenda**selezionare la riga vuota nell'elenco a discesa. Per il momento, gli intervalli di colore saranno visualizzati solo nella scala dei colori.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 La scala dei colori visualizza cinque colori: rosso, arancione, giallo, verde bottiglia chiaro e verde. Ogni colore rappresenta un intervallo di vendite che viene calcolato automaticamente in base alle vendite di ogni regione.  
  
###  <a name="ColorScale"></a> 6c. Formattare i dati nella scala dei colori come valuta  
 Per impostazione predefinita, i dati presentano un formato generale. È possibile applicare formati personalizzati.  
  
##### <a name="to-set-the-format-for-the-color-scale"></a>Per impostare il formato per la scala dei colori  
  
1.  Fare doppio clic la scala dei colori e quindi fare clic su **proprietà scala dei colori**.  
  
2.  Fare clic su **numero**.  
  
3.  Nelle **categoria**, fare clic su **valuta**.  
  
4.  Nelle **posizioni decimali**, digitare **0**. Questo formato non specifica alcuna cifra decimale per la valuta.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Visualizzare l'anteprima del report.  
  
 La scala dei colori visualizza le vendite annuali nel formato della valuta per ogni intervallo.  
  
###  <a name="NewLegend"></a> 6d. Creare una nuova legenda  
 Per impostazione predefinita, tutte le regole vengono visualizzate nella prima legenda. Per migliorare la visualizzazione per una mappa, è possibile aggiungere legende.  
  
 Per modificare la visualizzazione predefinita, è possibile eseguire due passaggi: creare una nuova legenda e quindi associare i risultati della regola per un livello mappa alla nuova legenda.  
  
##### <a name="to-create-a-new-legend"></a>Per creare una nuova legenda  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic all'esterno del viewport della mappa e quindi fare clic su **Aggiungi legenda**. Una nuova legenda viene aggiunta alla mappa in una posizione predefinita.  
  
3.  Fare doppio clic la legenda e quindi fare clic su **proprietà legenda**.  
  
4.  Nelle **posizionare opzioni**, fare clic sul percorso che specifica in cui si desidera visualizzare rispetto al viewport la legenda. La mappa sull'area di progettazione cambia al fine di mostrare l'effetto delle selezioni.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Fare clic su **titolo** sulla legenda per selezionare il titolo della legenda.  
  
7.  Fare clic su **titolo** nuovamente alla modalità di inserimento per il testo. Sostituire **Title** dal **vendite (migliaia)** e quindi fare clic all'esterno del testo.  
  
 La legenda si espande per visualizzare il titolo.  
  
###  <a name="Associate"></a> 6e. Associare la legenda e le regole colori  
 Ogni legenda può visualizzare uno o più set di risultati della regola.  
  
##### <a name="to-associate-a-legend-with-color-rules"></a>Per associare una legenda alle regole colori  
  
1.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
2.  Fare clic sulla freccia in giù in PolygonLayer1 e quindi fare clic su **regola colore poligono**. Viene visualizzata la finestra di dialogo **Proprietà regole colori mappa** .  
  
3.  Fare clic su **Legenda**.  
  
4.  Nelle **Opzioni scala dei colori**deselezionare **Mostra nella scala dei colori**.  
  
5.  Nelle **Opzioni legenda**, nell'elenco a discesa, selezionare Legend2. Viene visualizzata l'opzione del testo della legenda. Per impostazione predefinita, il testo della legenda viene formattato con una stringa di formato [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] generale. Gli 0 in N0 indicano nessuna cifra decimale.  
  
6.  Nelle **testo della legenda**, usare il formato seguente per specificare la valuta senza cifre decimali: `#FROMVALUE {C0} - #TOVALUE {C0}`  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Sull'area di progettazione la legenda visualizza gli intervalli di colori con dati di esempio formattati come valuta.  
  
8.  Visualizzare l'anteprima del report.  
  
 Le regioni a cui sono associati negozi e vendite vengono visualizzate in base alle regole colori. Le regioni a cui non sono associate vendite non presentano colori.  
  
###  <a name="NoData"></a> 6f. Modificare il colore per le regioni prive di dati  
 È possibile impostare le opzioni di visualizzazione predefinite per tutti gli elementi della mappa su un livello. Le regole colori hanno la precedenza su queste opzioni di visualizzazione.  
  
##### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Per impostare le proprietà di visualizzazione per tutti gli elementi su un livello  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** .  
  
3.  Fare clic sulla freccia giù per PolygonLayer1, quindi su **Proprietà poligono**. Viene visualizzata la finestra di dialogo **Proprietà poligono mappa** . Le opzioni di visualizzazione impostate in questa finestra di dialogo sono applicabili a tutti i poligoni del livello prima che vengano applicate le opzioni di visualizzazione basate su regola.  
  
4.  Fare clic su **riempire**.  
  
5.  Verificare che lo stile di riempimento sia **a tinta unita.** Le sfumature e i modelli si applicano a tutti i colori.  
  
6.  Nelle **colore**, fare clic sulla freccia verso il basso e quindi fare clic su **acciaio chiaro**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualizzare l'anteprima del report.  
  
 Le regioni a cui non sono associati dati vengono visualizzate in blu. Solo le regioni a cui sono associati dati analitici vengono visualizzati nei **rosso** attraverso **verde** colori dalle regole colore specificato.  
  
##  <a name="CustomPoint"></a> 7. Aggiungere un punto personalizzato  
 Per rappresentare un nuovo Negozio che non è ancora stato compilato, specificare un punto e usare la **puntina da disegno** tipo di marcatore.  
  
#### <a name="to-add-a-custom-point"></a>Per aggiungere un punto personalizzato  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare doppio clic sulla mappa per visualizzare il riquadro **Livello mappa** . Sulla barra degli strumenti, fare clic su **Aggiungi livello**, quindi fare clic su **livello punto**.  
  
     Un nuovo livello punto viene aggiunto alla mappa. Per impostazione predefinita, il livello punto usa il tipo di dati spaziali **Incorporato**.  
  
3.  Fare clic sulla freccia in giù in PointLayer2 e quindi fare clic su **Aggiungi punto**.  
  
4.  Spostare il puntatore sul viewport mappa. Il cursore passa alla selezione di precisione.  
  
5.  Fare clic sulla posizione sulla mappa in cui si desidera aggiungere un punto. In questa esercitazione fare clic su una posizione in una regione accanto all'inizio dell'itinerario. Un punto contrassegnato da un cerchio viene aggiunto al livello nella posizione selezionata. Per impostazione predefinita, il punto viene selezionato.  
  
6.  Fare clic con il pulsante destro del mouse sul punto aggiunto, quindi scegliere **Proprietà punto incorporato**.  
  
7.  Selezionare l'opzione **Ignora opzioni punto per questo livello**. Nella finestra di dialogo vengono visualizzate pagine aggiuntive. I valori impostati qui hanno la precedenza sulle opzioni di visualizzazione per il livello o per le regole colori.  
  
8.  Fare clic su **marcatore**.  
  
9. Per la **tipo di marcatore**, selezionare **Star**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Visualizzare l'anteprima del report.  
  
 Il nuovo punto aggiunto viene visualizzato come un **Star**.  
  
#### <a name="to-add-a-label-for-the-custom-point"></a>Per aggiungere un'etichetta per il punto personalizzato  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic sul punto appena aggiunto e quindi fare clic su **proprietà punto incorporato**.  
  
3.  Fare clic su **etichette**.  
  
4.  Nelle **testo dell'etichetta**, digitare **Store New**.  
  
5.  In **Posizione**fare clic su **Torna all'inizio**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualizzare l'anteprima del report.  
  
 L'etichetta viene visualizzata sopra la posizione del negozio.  
  
##  <a name="CenterView"></a> Allineare al centro la vista mappa  
 Modificare livello di allineamento al centro e zoom del viewport mappa.  
  
#### <a name="to-change-the-viewport"></a>Per modificare il viewport  
  
1.  Pulsante destro del mouse sul viewport mappa e quindi fare clic su **proprietà Viewport**.  
  
2.  Fare clic su **al centro e Zoom**.  
  
3.  Verificare che l'opzione **impostato a livello di una visualizzazione centro e zoom della** sia selezionata.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare clic con il pulsante sinistro del mouse sul viewport mappa e trascinarne il centro fino al punto desiderato.  
  
6.  Utilizzare la rotella del mouse per modificare il livello di zoom del viewport.  
  
7.  Visualizzare l'anteprima del report.  
  
 Nella visualizzazione della struttura la mappa nell'area di visualizzazione e la visualizzazione sono basate su dati di esempio. Nel report visualizzabile, la vista mappa è allineata al centro della vista specificata.  
  
##  <a name="Title"></a> Aggiungere un titolo al Report  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite nei punti vendita di New York** , quindi fare clic all'esterno della casella di testo.  
  
 Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
##  <a name="Save"></a> Salvare il Report  
  
#### <a name="to-save-the-report"></a>Per salvare il report  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Dal pulsante Generatore report fare clic su **Salva con nome**.  
  
3.  In **Nome**digitare **Punti vendita di New York - vendite**.  
  
 Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Questa operazione conclude la procedura dettagliata per l'aggiunta di una mappa al report.  
  
 Per altre informazioni, vedere [Maps &#40;Generatore Report e SSRS&#41; ](report-design/maps-report-builder-and-ssrs.md) e il post di blog [Cartographic Adjustment of Spatial Data per SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=152771) sul sito Web blogs.msdn.com.  
  
 Per altre esercitazioni, vedere [esercitazioni &#40;Generatore Report&#41;](report-builder-tutorials.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)   
 [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
