---
title: Modificare legende della mappa, scala dei colori e regole associate (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql13.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- sql13.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql13.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10534"
- "10516"
- sql13.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10514"
- sql13.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- "10513"
- sql13.rtp.rptdesigner.shared.mapruleslegend.f1
- sql13.rtp.rptdesigner.shared.embeddedlabels.f1
- "10510"
- "10509"
- sql13.rtp.rptdesigner.maplegendproperties.general.f1
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c4b71175eb95acf68f1f7a6d0eb2a2e23f609006
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134282"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>Modificare legende della mappa, scala dei colori e regole associate (Generatore report e SSRS)
  In un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] una mappa può includere legende, una scala dei colori e una scala distanza. Questi parti di una mappa consentono agli utenti di interpretare la visualizzazione dei dati sulla mappa.  
  
 Le legende includono le parti seguenti di una mappa:  
  
-   **Legenda mappa** Visualizza una guida che agevola l'interpretazione dei dati analitici che variano la visualizzazione degli elementi di una mappa su un livello mappa. Una mappa può presentare più legende. Per ogni livello mappa, specificare quale legenda utilizzare. Una legenda può fornire una guida a più di un livello mappa.  
  
-   **Scala dei colori** Visualizza una guida che agevola l'interpretazione dei colori sulla mappa. Una mappa dispone di una scala dei colori. Più livelli possono fornire i dati per la scala dei colori.  
  
-   **Scala distanza** Visualizza una guida che agevola l'interpretazione della scala della mappa. Una mappa dispone di una scala distanza. Il valore di zoom corrente del viewport mappa determina la scala distanza.  
  
 ![rs_MapElements](../../reporting-services/report-design/media/rs-mapelements.gif "rs_MapElements")  
  
##  <a name="Viewport"></a> Per modificare la posizione di una legenda rispetto al viewport  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>Per modificare la posizione di una legenda rispetto al viewport  
  
1.  In visualizzazione Struttura fare clic con il pulsante destro del mouse sulla legenda e aprire la pagina **Proprietà** _\<elemento report>_.  
  
2.  In **Posizione**fare clic sulla posizione che specifica il punto in cui visualizzare la legenda rispetto al viewport.  
  
3.  Per visualizzare la legenda al di fuori del viewport, selezionare **Mostra elemento del report>\< al di fuori del viewport**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Nell'anteprima, le legende della mappa e la scala dei colori vengono visualizzate solo se sono disponibili i risultati delle regole correlate a tale legenda. Se non vi sono elementi da visualizzare, la legenda non viene mostrata nel report di cui è stato eseguito il rendering.  
  
##  <a name="MapLegend"></a> Per modificare il layout della legenda di una mappa  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>Per modificare il layout della legenda di una mappa  
  
1.  Nella visualizzazione struttura fare clic con il pulsante destro del mouse sulla legenda e aprire la pagina **Proprietà legenda** .  
  
2.  In **Layout legenda**fare clic sul layout della tabella da usare per la legenda. Selezionando opzioni diverse, il layout sull'area di progettazione cambia.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="MapLegendTitle"></a> Per mostrare o nascondere il titolo della legenda di una mappa  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>Per mostrare o nascondere il titolo della legenda di una mappa  
  
-   Fare clic con il pulsante destro del mouse sulla legenda della mappa nell'area di progettazione e quindi scegliere **Mostra titolo legenda**.  
  
##  <a name="ColorScaleTitle"></a> Per mostrare o nascondere il titolo della scala dei colori  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>Per mostrare o nascondere il titolo della scala dei colori  
  
-   Fare clic con il pulsante destro del mouse sulla scala dei colori nell'area di progettazione e quindi scegliere **Mostra titolo scala dei colori**.  
  
##  <a name="MoveItems"></a> Per spostare elementi all'esterno della prima legenda  
 Creare il numero di legende aggiuntive desiderato, quindi aggiornare le regole per ogni livello mappa per specificare in quale legenda visualizzare i risultati delle regole.  
  
#### <a name="to-create-a-new-legend"></a>Per creare una nuova legenda  
  
-   Nella visualizzazione della struttura fare clic con il pulsante destro del mouse sulla mappa all'esterno del viewport e quindi scegliere **Aggiungi legenda**.  
  
     Una nuova legenda verrà visualizzata sulla mappa.  
  
#### <a name="to-display-rule-results-in-a-legend"></a>Per visualizzare i risultati delle regole in una legenda  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che contiene i dati desiderati e quindi scegliere _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Fare clic su **Legenda**.  
  
4.  Nell'elenco a discesa **Mostra in questa legenda** fare clic sul nome della legenda in cui visualizzare i risultati della regola.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TemplateStyle"></a> Per variare i colori degli elementi della mappa in base a uno stile modello  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>Per variare i colori degli elementi della mappa in base a uno stile modello  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che contiene i dati desiderati e quindi scegliere _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Fare clic su **Applica stile modello**.  
  
     Uno stile modello consente di specificare lo stile del carattere e del bordo, nonché la tavolozza colori. A ogni elemento della mappa viene assegnato un colore diverso dall'apposita tavolozza per il tema specificato nella Creazione guidata mappa o Creazione guidata livello mappa. Si tratta dell'unica opzione che si applica ai livelli che non dispongono di dati analitici associati.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorPalette"></a> Per variare i colori degli elementi della mappa in base a una tavolozza colori  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>Per variare i colori degli elementi della mappa in base a una tavolozza colori  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che dispone dei dati desiderati e quindi selezionare _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Fare clic su **Visualizza dati tramite tavolozza colori**.  
  
     Questa opzione consente di utilizzare una tavolozza predefinita o personalizzata specificata. A seconda dei dati analitici correlati, a ogni elemento della mappa viene assegnato un colore o una sfumatura di colore diverso dalla tavolozza.  
  
4.  In **Campo dati**digitare il nome del campo che contiene i dati analitici da visualizzare per colore.  
  
5.  In **Tavolozza**selezionare il nome della tavolozza da usare nell'elenco a discesa.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorRanges"></a> Per variare i colori degli elementi della mappa in base a intervalli di colori  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>Per variare i colori degli elementi della mappa in base a intervalli di colori  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che dispone dei dati desiderati e quindi selezionare _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Fare clic su **Visualizza dati tramite intervalli colori**.  
  
     Questa opzione, combinata con i colori iniziale, intermedio e finale indicati in questa pagina e le opzioni che si specificano nella pagina **Distribuzione** , consentono di dividere i dati analitici correlati in intervalli. L'elaboratore di report assegna il colore adatto a ogni elemento della mappa in base ai relativi dati associati e all'intervallo di cui fa parte.  
  
4.  In **Campo dati**digitare il nome del campo che contiene i dati analitici da visualizzare per colore.  
  
5.  In **Colore iniziale**specificare il colore da usare per l'intervallo minimo.  
  
6.  In **Colore intermedio**specificare il colore da usare per l'intervallo intermedio.  
  
7.  In **Colore finale**specificare il colore da usare per l'intervallo massimo.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="CustomColors"></a> Per variare i colori degli elementi della mappa in base a colori personalizzati  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>Per variare i colori degli elementi della mappa in base a colori personalizzati  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che dispone dei dati desiderati e quindi selezionare _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Fare clic su **Visualizza dati tramite colori personalizzati**.  
  
     Questa opzione consente di utilizzare l'elenco di colori specificato. A seconda dei dati analitici correlati, a ogni elemento della mappa viene assegnato un colore dell'elenco. Se il numero di elementi della mappa è maggiore dei colori disponibili, non viene assegnato nessun colore.  
  
4.  In **Campo dati**digitare il nome del campo che contiene i dati analitici da visualizzare per colore.  
  
5.  In **Colori personalizzati**fare clic su **Aggiungi** per specificare ogni colore personalizzato.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="DistributionOptions"></a> Per impostare opzioni di distribuzione per una legenda  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>Per impostare opzioni di distribuzione per una legenda  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che dispone dei dati desiderati e quindi selezionare _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Selezionare l'opzione **Visualizza dati tramite** \<tipo di regola>. Per usare le opzioni di distribuzione, è necessario creare intervalli nella pagina **Distribuzione** in base ai dati analitici associati al livello.  
  
4.  Fare clic su **Distribuzione**.  
  
5.  Selezionare uno dei seguenti tipi di distribuzione:  
  
    -   **Intervallo equo**. Specifica gli intervalli che dividono i dati in intervalli equi.  
  
    -   **Distribuzione equa**. Specifica gli intervalli che dividono i dati in modo che ogni intervallo disponga di un numero uguale di elementi.  
  
    -   **Ottimale**. Specifica gli intervalli che regolano automaticamente la distribuzione per creare intervalli secondari equilibrati.  
  
    -   **Personalizzato**. Specifica il numero di intervalli per controllare la distribuzione di valori.  
  
     Per altre informazioni sulle opzioni di distribuzione, vedere [Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
6.  In **Numero di intervalli secondari**digitare il numero di intervalli secondari da usare. Se il tipo di distribuzione è **Ottimale**, il numero di intervalli secondari viene calcolato automaticamente.  
  
7.  In **Inizio intervallo**digitare un valore di intervallo minimo. Tutti i valori inferiori a questo numero corrispondono al minimo dell'intervallo.  
  
8.  In **Fine intervallo**digitare un valore di intervallo massimo. Tutti i valori superiori a questo numero corrispondono al massimo dell'intervallo.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="RuleLegend"></a> Per modificare il contenuto di una legenda di regole  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>Per modificare il contenuto di una legenda di tipo dimensioni, spessore o tipo di marcatore  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che contiene i dati desiderati e quindi scegliere **Regola** _\<tipo di elemento mappa>_.  
  
3.  Verificare che l'opzione **Visualizza dati tramite** \<*tipo di regola*> sia selezionata.  
  
4.  In **Campo dati**verificare che vengano selezionati i dati analitici visualizzati sul livello.  
  
    > [!NOTE]  
    >  Se nell'elenco a discesa non viene visualizzato alcun campo, fare clic con il pulsante destro del mouse sul livello, scegliere **Dati livello** per aprire la pagina Dati analitici della finestra di dialogo Proprietà dati livello mappa e verificare che siano stati specificati i dati analitici per questo livello.  
  
5.  Fare clic su **Legenda**.  
  
6.  In **Mostra in questa legenda**selezionare la legenda della mappa da usare per visualizzare i risultati della regola.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ColorScale"></a> Per modificare il contenuto della scala dei colori  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>Per modificare il contenuto della legenda della scala dei colori o dei colori  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che dispone dei dati desiderati e quindi selezionare _\<tipo di elemento mappa>_**Regola colore**.  
  
3.  Selezionare l'opzione della regola colore da utilizzare. Per visualizzare gli elementi in una legenda della mappa o in una scala dei colori, è necessario selezionare una delle opzioni **Visualizza dati tramite** tipo di regola>\<.  
  
4.  In **Campo dati**verificare che vengano selezionati i dati analitici visualizzati sul livello.  
  
    > [!NOTE]  
    >  Se nell'elenco a discesa non viene visualizzato alcun campo, fare clic con il pulsante destro del mouse sul livello, scegliere **Dati livello** per aprire la pagina Dati analitici della finestra di dialogo Proprietà dati livello mappa e verificare che siano stati specificati i dati analitici per questo livello.  
  
5.  Fare clic su **Legenda**.  
  
6.  In **Opzioni scala dei colori**selezionare **Mostra nella scala dei colori** per visualizzare i risultati della regola nella scala dei colori. Questa opzione può essere specificata per più di una regola colore.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="HideItems"></a> Per rimuovere tutti gli elementi da una legenda  
  
#### <a name="to-hide-items-based-on-a-rule"></a>Per nascondere elementi in base a una regola  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che contiene i dati desiderati e quindi scegliere **Regola** _\<tipo di elemento mappa>_.  
  
3.  Fare clic su **Legenda**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ChangeFormatItems"></a> Per modificare il formato del contenuto in una legenda  
 Impostare le opzioni legenda per la regola associata alla legenda della mappa.  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>Per modificare il formato del contenuto in una legenda  
  
1.  In visualizzazione struttura fare clic sulla mappa finché non viene visualizzato il riquadro della mappa.  
  
2.  Fare clic con il pulsante destro del mouse sul livello che contiene i dati desiderati e quindi scegliere **Regola** _\<tipo di elemento mappa>_.  
  
3.  Fare clic su **Legenda**.  
  
4.  **Testo legenda** visualizza le parole chiave che specificano quali dati compaiono nella legenda. Utilizzare parole chiave e formati personalizzati per controllare il formato del testo della legenda. Ad esempio, #FROMVALUE {C2} specifica un formato valuta con due cifre decimali. Per altre informazioni, vedere [Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Mappe &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Aggiungere, modificare o eliminare una mappa o un livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Risolvere problemi relativi ai report: Report mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
