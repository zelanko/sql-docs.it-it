---
title: Aggiungere, modificare o eliminare una mappa o un livello mappa (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10526"
- sql12.rtp.rptdesigner.maptilelayerproperties.general.f1
- "10529"
- "10525"
- "10535"
- sql12.rtp.rptdesigner.mappolygonlayerproperties.general.f1
- sql12.rtp.rptdesigner.shared.layervisibility.f1
- sql12.rtp.rptdesigner.mappointlayerproperties.general.f1
- sql12.rtp.rptdesigner.shared.layerfilters.f1
- "10524"
- sql12.rtp.rptdesigner.maplayerproperties.general.f1
- sql12.rtp.rptdesigner.maplinelayerproperties.general.f1
- "10532"
- "10528"
- "10527"
- sql12.rtp.rptdesigner.maplayerproperties.analyticaldata.f1
ms.assetid: 6e89815e-187e-45bf-bf63-3d5c4a246360
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 13a67a94f6478c085995142085a93fa85bb27d89
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106708"
---
# <a name="add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs"></a>Aggiungere, modificare o eliminare una mappa o un livello mappa (Generatore report e SSRS)
  Una mappa è una raccolta di livelli. Quando si aggiunge una mappa a un report, si definisce il primo livello. È possibile creare livelli aggiuntivi tramite la creazione guidata del livello mappa.  
  
 Il modo più semplice per aggiungere, rimuovere o modificare le opzioni per un livello è utilizzare la creazione guidata del livello mappa. È possibile inoltre modificare manualmente le opzioni dal riquadro della mappa. Per visualizzare il riquadro **Mappa** , fare clic nella mappa sull'area di progettazione del report. Nella figura seguente vengono visualizzate le parti del riquadro:  
  
 ![rsMapLayerZone](../media/rsmaplayerzone.gif "rsMapLayerZone")  
  
 I livelli mappa vengono disegnati dal basso verso l'alto nell'ordine in cui vengono visualizzati nel riquadro della mappa. Nella figura precedente, viene disegnato per primo il livello sezione e per ultimo il livello poligono. I livelli disegnati in un secondo momento potrebbero nascondere elementi della mappa di livelli disegnati in precedenza. È possibile modificare l'ordine dei livelli tramite i tasti di direzione sulla barra degli strumenti del riquadro della mappa. Per mostrare o nascondere i livelli, attivare o disattivare l'icona della visibilità. È possibile modificare la trasparenza di un livello nella `Visibility` pagina della finestra di dialogo proprietà **dati livello** .  
  
 Nella tabella seguente vengono visualizzate le icone della barra degli strumenti per il riquadro **Mappa** .  
  
|Simbolo|Descrizione|Utilizzo|  
|------------|-----------------|-----------------|  
|![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")|Creazione guidata livello mappa|Per aggiungere un livello tramite una procedura guidata, fare clic su **Creazione guidata nuovo livello**.|  
|![rs_IconMapAddLayer](../../tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")|Aggiungi livello|Per aggiungere manualmente un livello, fare clic su **Aggiungi livello**, quindi scegliere il tipo di livello mappa da aggiungere.|  
|![rs_IconMapPolygonLayer](../media/rs-iconmappolygonlayer.gif "rs_IconMapPolygonLayer")|Livello poligono|Per aggiungere un livello mappa che visualizza aree o forme basate su set di coordinate del poligono.|  
|![rs_IconMapLineLayer](../media/rs-iconmaplinelayer.gif "rs_IconMapLineLayer")|Livello linea|Per aggiungere un livello mappa che visualizza percorsi o itinerari basati su set di coordinate della linea.|  
|![rs_IconMapPointLayer](../media/rs-iconmappointlayer.gif "rs_IconMapPointLayer")|Livello punto|Per aggiungere un livello mappa che visualizza posizioni basate su set di coordinate del punto.|  
|![rs_IconMapTileLayer](../media/rs-iconmaptilelayer.gif "rs_IconMapTileLayer")|Livello sezione|Per aggiungere un livello mappa che visualizza le tessere mappa di Bing che corrispondono all'area della vista mappa corrente definita dal viewport.|  
  
 Nella parte inferiore del riquadro della mappa si trova l'area della vista mappa. Per modificare le opzioni di allineamento al centro o zoom della mappa, utilizzare i tasti di direzione in modo da regolare il centro della vista e il dispositivo di scorrimento che consente di modificare il livello di zoom.  
  
 Per altre informazioni sui livelli, vedere [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="to-add-a-layer-from-the-map-layer-wizard"></a><a name="AddLayer"></a> Per aggiungere un livello dalla Creazione guidata livello mappa  
  
-   Nel menu **Inserisci** della barra multifunzione fare clic su **Mappa**, quindi scegliere **Creazione guidata mappa.** La procedura guidata consente di aggiungere un livello alla mappa esistente. La maggior parte delle pagine della Creazione guidata mappa e della Creazione guidata livello mappa sono identiche.  
  
     Per altre informazioni, vedere [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  

##  <a name="to-change-options-for-a-layer-by-using-the-map-layer-wizard"></a><a name="ChangeLayer"></a> Per modificare le opzioni di un livello tramite la Creazione guidata livello mappa  
  
-   Eseguire la Creazione guidata livello mappa. Questa procedura guidata consente di modificare le opzioni per un livello creato tramite la Creazione guidata livello mappa. Nel riquadro Mappa fare clic con il pulsante destro del mouse sul livello, quindi fare clic sul pulsante della creazione guidata del livello sulla barra degli strumenti (![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")).  
  
     Per altre informazioni, vedere [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  

##  <a name="to-add-a-point-line-or-polygon-layer-from-the-map-pane-toolbar"></a><a name="AddVectorLayer"></a> Per aggiungere un livello punto, linea o poligono dalla barra degli strumenti del riquadro della mappa  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Nella barra degli strumenti fare clic sul pulsante **Aggiungi livello** e, dall'elenco a discesa, scegliere il tipo di livello da aggiungere: **Punto**, **Linea** o **Poligono**.  
  
    > [!NOTE]  
    >  Sebbene sia possibile aggiungere un livello alla mappa e configurarlo manualmente, è consigliabile utilizzare la Creazione guidata livello mappa per aggiungere nuovi livelli. Per avviare la procedura guidata dal riquadro Mappa della barra degli strumenti, fare clic sul pulsante della creazione guidata del livello (![rs_IconMapLayerWizard](../../tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")).  
  
3.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Dati livello**.  
  
4.  In **Usa dati spaziali da**selezionare l'origine dati spaziali. Le opzioni variano in base alla selezione.  
  
     Se si desidera visualizzare i dati analitici del report su questo livello, eseguire le operazioni seguenti:  
  
    1.  Fare clic su **Dati analitici**.  
  
    2.  In **Set di dati analitici**fare clic sul nome del set di dati che contiene i dati analitici e i campi delle corrispondenze per compilare una relazione tra i dati analitici e quelli spaziali.  
  
    3.  Scegliere **Aggiungi**.  
  
    4.  Digitare il nome del campo delle corrispondenze del set di dati spaziali.  
  
    5.  Digitare il nome del campo delle corrispondenze del set di dati analitici.  
  
     Per altre informazioni sul collegamento di dati spaziali e analitici, vedere [Personalizzazione dei dati e visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-filter-analytical-data-for-the-layer"></a><a name="FilterAnalyticalData"></a> Per filtrare dati analitici per il livello  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello nel riquadro della mappa, quindi scegliere  **Dati livello**.  
  
3.  Fare clic su **Filtri**.  
  
4.  Definire un'equazione di filtro per limitare i dati analitici utilizzati nella vista mappa. Per altre informazioni, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md).  

##  <a name="to-control-point-properties-for-a-point-layer-or-for-polygon-center-points"></a><a name="PointProperties"></a> Per controllare le proprietà punto per un livello punto o per i punti centrali del poligono  
  
1.  Selezionare **Generale** nella finestra di dialogo **Proprietà punto mappa** per modificare le opzioni relative all'etichetta, alla descrizione comando e al tipo di indicatore per gli elementi della mappa seguenti:  
  
    -   Tutti i punti dinamici o incorporati su un livello punto. Le regole relative al colore, alle dimensioni e al tipo di marcatore per i punti ignorano queste opzioni. Per sostituire le opzioni per un punto incorporato specifico, usare la pagina [Finestra di dialogo Proprietà punto incorporato mappa, Indicatore](../map-embedded-point-properties-dialog-box-marker.md) .  
  
    -   Punto centrale per tutti i poligoni dinamici o incorporati su un livello poligono. Le regole relative al colore, alle dimensioni e al tipo di marcatore per i punti centrali ignorano queste opzioni. Per sostituire le opzioni per un punto centrale specifico, usare la pagina [Finestra di dialogo Proprietà punto incorporato mappa, Indicatore](../map-embedded-point-properties-dialog-box-marker.md) .  

##  <a name="to-specify-embedded-data-as-a-source-of-spatial-data"></a><a name="Embedded"></a> Per specificare i dati incorporati come origine di dati spaziali  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Dati livello**.  
  
3.  In **Usa dati spaziali da**selezionare **Dati incorporati nel report**.  
  
4.  Per caricare gli elementi della mappa da un report esistente o creare elementi della mappa basati su un file ESRI, fare clic su **Sfoglia**, scegliere il file, quindi scegliere **Apri**. Gli elementi della mappa vengono incorporati in questa definizione del report. I dati spaziali scelti devono corrispondere al tipo di livello. Ad esempio per un livello punto, è necessario scegliere i dati spaziali che specificano set di coordinate del punto.  
  
5.  In **Campo spaziale**specificare il nome del campo che contiene dati spaziali. Potrebbe essere necessario determinare questo nome dall'origine dati spaziali.  
  
    > [!NOTE]  
    >  Se non si conosce il nome del campo ed è stato selezionato un file di forma ESRI, usare l'opzione **Collegamento a file di forma ESRI** anziché questa opzione.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-specify-an-esri-shapefile-as-a-source-of-spatial-data"></a><a name="ESRI"></a> Per specificare un file di forma ESRI come origine di dati spaziali  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Dati livello**.  
  
3.  In **Usa dati spaziali da**selezionare **Collegamento a file di forma ESRI**.  
  
4.  In **Nome file**digitare il percorso di un file di forma ESRI o fare clic su **Sfoglia** per selezionare un file di forma ESRI.  
  
    > [!NOTE]  
    >  Se il file di forma si trova sul computer locale, i dati spaziali sono incorporati nella definizione del report. Per recuperare in modo dinamico i dati durante l'elaborazione del report, è necessario caricare il file ESRI con estensione shp e il file di supporto con estensione dbf sul server di report. Per altre informazioni, vedere "Procedura: Caricamento di un file o di un report (Gestione report)" nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di SQL Server.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-specify-a-report-dataset-field-as-a-source-of-spatial-data"></a><a name="DatasetField"></a> Per specificare un campo del set di dati del report come origine di dati spaziali  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Dati livello**.  
  
3.  In **Usa dati spaziali da**selezionare **Campo spaziale in un set di dati**.  
  
4.  In **Nome set di dati**fare clic sul nome di un set di dati del report che contiene i dati spaziali desiderati.  
  
5.  In **Nome campo spaziale**fare clic sul nome del campo del set di dati che contiene i dati spaziali.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-add-a-tile-layer"></a><a name="TileLayer"></a> Per aggiungere un livello sezione  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Sulla barra degli strumenti fare clic sul pulsante **Aggiungi livello** e, dall'elenco a discesa, scegliere **Livello sezione**.  
  
    > [!NOTE]  
    >  Per altre informazioni sull'utilizzo delle tessere mappa di Bing nel report, vedere [Ulteriori condizioni di utilizzo](https://go.microsoft.com/fwlink/?LinkId=151371) e [Informativa sulla privacy](https://go.microsoft.com/fwlink/?LinkId=151372).  
  
3.  Fare clic con il pulsante destro del mouse sul livello sezione nel riquadro della mappa, quindi scegliere **Proprietà sezione**.  
  
4.  In **Opzioni sezioni**selezionare uno stile della sezione. Se sono disponibili le tessere mappa di Bing, il livello sull'area di progettazione viene aggiornato con lo stile selezionato.  
  
    > [!NOTE]  
    >  Un livello sezione può essere aggiunto anche quando si aggiunge un livello poligono, linea o punto nella Creazione guidata mappa o Creazione guidata livello mappa. Nella pagina **Scegli opzioni di dati spaziali e vista mappa** selezionare l'opzione **Add a Bing Maps background for this map view (Aggiungi sfondo Bing Maps per la vista mappa)** .  

##  <a name="to-change-the-drawing-order-of-a-layer"></a><a name="DrawingOrder"></a> Per modificare l'ordine di disegno di un livello  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic sul livello nel riquadro della mappa per selezionarlo.  
  
3.  Sulla barra degli strumenti del riquadro della mappa fare clic sulla freccia in su o in giù per modificare l'ordine di disegno di ogni livello.  

##  <a name="to-change-the-transparency-of-a-polygon-line-or-point-layer"></a><a name="Transparency"></a> Per modificare la trasparenza di un livello poligono, linea o punto  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Dati livello**.  
  
3.  Fare clic su `Visibility`.  
  
4.  In **Opzioni trasparenza**digitare un valore che rappresenta la percentuale di trasparenza, ad esempio **40**. La trasparenza zero (0) % significa che il livello è opaco. Trasparenza 100% significa che il livello non sarà visibile nel report.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-change-the-transparency-of-a-tile-layer"></a><a name="TileTransparency"></a> Per modificare la trasparenza di un livello sezione  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello, quindi scegliere **Proprietà sezione**.  
  
3.  Fare clic su `Visibility`.  
  
4.  In **Opzioni trasparenza**digitare un valore che rappresenta la percentuale di trasparenza, ad esempio **40**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

##  <a name="to-specify-a-secure-connection-for-a-tile-layer"></a><a name="Secure"></a> Per specificare una connessione protetta per un livello sezione  
  
1.  Fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Nel riquadro della mappa fare clic sul livello sezione per selezionarlo. Nel riquadro Proprietà verranno visualizzate le proprietà del livello sezione.  
  
3.  Nel riquadro Proprietà impostare UseSecureConnection su **True**.  
  
 La connessione per il servizio Web di Bing Maps utilizzerà il servizio HTTP SSL (Secure Sockets Layer) per recuperare le tessere mappa di Bing per questo livello.  

##  <a name="to-specify-the-language-for-tile-labels"></a><a name="Language"></a> Per specificare la lingua per le etichette delle sezioni  
  
1.  Per impostazione predefinita, per gli stili delle sezioni che consentono di visualizzare le etichette, la lingua viene determinata in base alle impostazioni locali predefinite per Generatore report. È possibile personalizzare l'impostazione della lingua per le etichette delle sezioni come indicato di seguito.  
  
    -   Fare clic sulla mappa all'esterno del viewport per selezionare la mappa. Nel riquadro Proprietà per la proprietà TileLanguage, selezionare un valore della lingua dall'elenco a discesa.  
  
    -   Fare clic sullo sfondo del report per selezionare il report. Nel riquadro Proprietà per la proprietà Language, selezionare un valore della lingua dall'elenco a discesa.  
  
     La lingua delle etichette delle sezioni viene impostata in base all'ordine di precedenza seguente: Language delle proprietà del report, impostazioni locali predefinite per Generatore report e TileLanguage delle proprietà della mappa.  

##  <a name="to-conditionally-hide-a-layer-based-on-viewport-zoom-level"></a><a name="ConditionalHide"></a> Per nascondere un livello basato sul livello di zoom del viewport in base a specifiche condizioni  
  
1.  Impostare `Visibility` le opzioni per controllare la visualizzazione per un livello mappa.  
  
    -   Nel riquadro Livelli mappa fare clic con il pulsante destro del mouse su un livello per selezionarlo e sulla barra degli strumenti di Livelli mappa fare clic su Proprietà per aprire **Proprietà livello mappa**.  
  
    -   Fare clic su `Visibility`.  
  
    -   In Visibilità livello selezionare **Mostra o nascondi in base a un valore di zoom**.  
  
    -   Immettere i valori di zoom minimo e massimo per la visualizzazione del livello.  
  
    -   Facoltativa. Immettere un valore per la trasparenza.  
  
     Inoltre è possibile nascondere il livello in base a condizioni specifiche. Per altre informazioni, vedere [Nascondere un elemento &#40;Generatore report e SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md).  

## <a name="see-also"></a>Vedere anche  
 [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Risolvere problemi relativi ai report: Report mappa &#40;Generatore report e SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
