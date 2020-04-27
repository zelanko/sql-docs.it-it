---
title: Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10521"
- sql12.rtp.rptdesigner.shared.shadowdv.f1
- "10515"
- "10512"
- "10520"
- "10523"
- sql12.rtp.rptdesigner.mapgroupproperties.variables.f1
- sql12.rtp.rptdesigner.mapgroupproperties.filter.f1
- sql12.rtp.rptdesigner.shared.number.f1
- sql12.rtp.rptdesigner.shared.font.f1
- sql12.rtp.rptdesigner.mapgroupproperties.general.f1
- "10507"
ms.assetid: fdd9b994-d138-4990-a291-279b0249eb72
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3cc939ac63f1b53e2d2d24d70edc5fe0798bcc51
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106101"
---
# <a name="customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs"></a>Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa (Generatore report e SSRS)
  Dopo aver aggiunto una mappa o un livello mappa a un report utilizzando una procedura guidata, è possibile modificare il tipo di visualizzazione della mappa nel report. È possibile apportare dei miglioramenti tenendo in considerazione i concetti seguenti:  
  
-   Per facilitare l'interpretazione dei dati visualizzati su una mappa da parte degli utenti, è possibile aggiungere legende e una scala dei colori, nonché etichette e descrizioni comandi.  
  
-   Per rendere più semplice la lettura della mappa, modificare il centro e il livello di zoom, aggiungere una scala distanza e visualizzare una griglia di sfondo.  
  
-   Per facilitare il controllo del tempo per disegnare una mappa quando si esegue il report, è possibile regolare la risoluzione per semplificare gli elementi della mappa.  
  
-   È possibile incorporare gli elementi della mappa nella definizione del report, quindi modificare il tipo di visualizzazione dei singoli elementi. Ad esempio è possibile visualizzare la posizione dell'ufficio principale con una puntina da disegno e quelle secondarie con i cerchi.  
  
-   È possibile aggiungere aree personalizzate specificando espressioni di raggruppamento dati proprie.  
  
-   È possibile aggiungere una posizione personalizzata in un punto specificato su un livello mappa che dispone di punti incorporati. È possibile impostare il valore e le proprietà di visualizzazione per i punti personalizzati in modo indipendente dagli altri punti di un livello punto.  
  
-   Per ottenere un risultato più dettagliato, è possibile aggiungere collegamenti agli elementi della mappa su ogni livello selezionabile da un utente per aprire i report correlati.  
  
 Per altre informazioni su come migliorare un report, vedere [pianificazione di un report &#40;Generatore report&#41;](planning-a-report-report-builder.md).  
  
 Le opzioni di visualizzazione influiscono sull'aspetto di una mappa o delle parti di una mappa quando si visualizza il report. Alcune opzioni controllano l'aspetto della mappa, ad esempio i bordi e i caratteri o l'area rappresentata sulla mappa. Altre controllano il contenuto di ogni livello, ad esempio le dimensioni delle bolle, i tipi di marcatore, le etichette o le descrizioni comandi.  
  
 Un elemento di report mappa include le parti seguenti: la mappa stessa, un viewport mappa, un set di titoli, un set di legende (legenda, scala dei colori e scala distanza), un set di livelli, un set di elementi della mappa su ogni livello (poligoni o righe o punti). Utilizzare le informazioni delle sezioni seguenti per capire tramite quale finestra di dialogo delle proprietà controllare le opzioni di visualizzazione per le diverse parti di una mappa.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="change-options-for-the-map"></a><a name="Map"></a> Modificare le opzioni per la mappa  
 Su un elemento del report con mappe, è possibile controllare quanto segue:  
  
-   Aggiungere più titoli.  
  
-   Aggiungere più legende. Per modificare il contenuto di una legenda, è necessario creare legende aggiuntive e successivamente modificare le regole per specificare in quale legenda immettere i relativi elementi creati da ogni regola.  
  
-   Aggiungere più livelli.  
  
-   Nascondere o visualizzare la scala distanza o la scala dei colori.  
  
-   Conferire un effetto ottico di profondità specificando un'ombreggiatura.  
  
 Per modificare queste opzioni fare clic con il pulsante destro del mouse sulla mappa, scegliere **Mappa**e apportare quindi le modifiche.  
  
 
  
##  <a name="change-options-for-the-viewport"></a><a name="Viewport"></a> Modificare le opzioni per il viewport  
 Utilizzare le opzioni del viewport per modificare la vista della mappa visualizzata nel report.  
  
 L'origine dei dati spaziali potrebbe fornire più aree da visualizzare nel report di quelle necessarie. È possibile utilizzare il viewport per impostare il centro, il livello di zoom e ritagliare l'area per la mappa.  
  
 Per il viewport è possibile impostare le opzioni seguenti:  
  
-   Scegliere il sistema di coordinate e, per un sistema di coordinate geografico, scegliere la proiezione.  
  
-   Scegliere il centro per la mappa.  
  
-   Ritagliare la vista per la mappa.  
  
-   Impostare il livello di zoom.  
  
-   Risoluzione e semplificazione. Stabilire un equilibrio tra il tempo necessario per il disegno e le strutture dettagliate di linee e poligoni.  
  
 Per modificare queste opzioni, fare clic con il pulsante destro del mouse su viewport mappa, usare la [finestra di dialogo Proprietà viewport mappa, la pagina Generale](../map-viewport-properties-dialog-box-general.md) e le pagine correlate.  
  

  
##  <a name="change-options-for-the-legends"></a><a name="Legends"></a> Modificare le opzioni per le legende  
 Le legende consentono agli utenti di interpretare i dati di una mappa.  
  
 Per impostazione predefinita, tutte le regole specificate per un livello aggiungono elementi alla prima legenda. Inoltre, tutte le regole colore visualizzano valori nella scala dei colori.  
  
-   Per modificare le opzioni di visualizzazione della legenda, inclusa la sua posizione rispetto al viewport, impostare le opzioni sulla legenda stessa.  
  
-   Per cambiare il contenuto o il relativo formato per una legenda, modificare le opzioni della legenda per le regole corrispondenti per un livello.  
  
 Per altre informazioni, vedere [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  

  
##  <a name="change-options-for-the-layer"></a><a name="Layer"></a> Modificare le opzioni per il livello  
 Per visualizzare i livelli per una mappa, fare clic sulla mappa per selezionarla. Viene visualizzato il riquadro della mappa. Per modificare le opzioni per un livello, fare clic con il pulsante destro del mouse sul livello e utilizzare il menu di scelta rapida.  
  
 Un livello può essere di tre tipi a seconda dei dati spaziali restituiti dalla relativa origine: un livello poligono, un livello linea o un livello punto.  
  
 Per il livello è possibile impostare le opzioni seguenti:  
  
-   I dati analitici e i campi delle corrispondenze associati. L'origine dei dati spaziali viene elencata nel riquadro della mappa sotto il nome del livello. Se l'origine è incorporata, gli elementi della mappa per il livello fanno parte della definizione del report. Se l'origine non è incorporata, i dati spaziali vengono recuperati in fase di esecuzione e l'elaboratore di report crea gli elementi della mappa per il livello durante l'elaborazione del report. Per modificare le opzioni dei dati sul livello, utilizzare la pagina Dati analitici nella finestra di dialogo del livello mappa.  
  
-   Ordine di disegno del livello. L'ordine secondo cui sono elencati i livelli nel riquadro della mappa è inverso rispetto all'ordine di disegno dei livelli. L'ultimo livello dell'elenco è quello disegnato per primo. Se si desidera, ad esempio, che i punti di un livello punto vengano visualizzati sopra i poligoni del relativo livello, il livello punto deve essere primo e il livello poligono secondo.  
  
-   Visibilità del livello, inclusa la trasparenza. Affinché un livello sia visibile attraverso un altro, impostare la trasparenza su un valore superiore a 0. Un valore pari a 100% significa che il livello non è visibile. Per usare un singolo livello, è sufficiente visualizzare o nascondere ciascun livello in modo indipendente tramite l'icona **Visibilità** nel riquadro della mappa. È inoltre possibile impostare le opzioni del livello di zoom per specificare quando visualizzare o nascondere gli elementi della mappa sul livello in base al livello di zoom.  
  
-   Aggiungere un livello tessera mappa di Bing per il livello di allineamento al centro e zoom del viewport corrente. Non è necessario specificare le coordinate geografiche per un livello sezione. Le sezioni vengono caricate automaticamente per ottenere una corrispondenza con l'area del viewport quando il sistema di coordinate è Geografico, la proiezione è Mercator, i server di Bing Maps sono disponibili e il server di report è stato configurato per supportare questa caratteristica. Per ogni report, è possibile specificare se utilizzare una connessione sicura per recuperare le sezioni.  
  
 Per altre informazioni sui livelli, vedere [aggiungere, modificare o eliminare una mappa o livello mappa &#40;Generatore report e SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="change-data-grouping-for-the-layer"></a><a name="DataGrouping"></a> Modificare il raggruppamento dati per il livello  
 È possibile personalizzare la modalità di aggregazione dei dati spaziali per forme proprie. Per impostare le proprietà di gruppo per un livello, selezionare il livello nel riquadro della mappa e nel riquadro Proprietà per il livello fare clic su **Gruppo** e quindi sui puntini di sospensione (...) per aprire Proprietà gruppo. In questa finestra di dialogo è possibile specificare le espressioni di raggruppamento, creare variabili di gruppo nonché filtrare dati utilizzati per il raggruppamento.  
  
 L'espressione di raggruppamento consente di specificare come vengono aggregati i dati analitici che hanno una relazione con i dati spaziali per ogni elemento della mappa sul livello. Per impostazione predefinita, l'espressione di raggruppamento è il set di campi delle corrispondenze specificato per la relazione tra i dati spaziali e i dati analitici. Ad esempio, per una mappa a bolle in cui sono visualizzati i percorsi delle città e le dimensioni della popolazione per regione o area, i campi delle corrispondenze includono il nome della città [Città] e il nome dell'area [Area] dal momento che possono esistere più città con lo stesso nome. Nell'espressione di raggruppamento corrispondente sono inclusi due campi: [City] e [Region].  
  
 Per altre informazioni, vedere la pagina relativa ai [suggerimenti sulle mappe relativi alle modalità di importazione dei file di forma in SQL Server e di aggregazione dei dati spaziali](https://go.microsoft.com/fwlink/?LinkID=214991).  
  
 
  
##  <a name="change-options-for-the-map-elements-on-the-layer"></a><a name="MapElements"></a> Modificare le opzioni per gli elementi della mappa sul livello  
 Gli elementi della mappa sono i punti, le linee o i poligoni di un livello basati sui dati spaziali. Per gli elementi della mappa è possibile impostare le opzioni seguenti. Queste opzioni si applicano a tutti gli elementi della mappa del livello indipendentemente se siano o meno incorporati:  
  
-   Etichette, visibilità e offset delle etichette e formattazione.  
  
-   Bordi e riempimento.  
  
-   Azioni di drill-through.  
  
-   Opzioni di visualizzazione.  
  
 Le opzioni di visualizzazione per gli elementi della mappa seguono un ordine di priorità basato sul livello, sull'elemento della mappa, sulle regole per l'elemento della mappa e sulle opzioni di sostituzione per gli elementi incorporati della mappa.  
  
 Per modificare queste opzioni, fare clic con il pulsante destro del mouse sull'elemento della mappa e utilizzare la finestra di dialogo delle proprietà incorporata. Ad esempio, per un poligono incorporato, utilizzare la pagina Generale della finestra di dialogo Proprietà poligono incorporato e le pagine correlate.  
  

  
##  <a name="understanding-display-option-precedence"></a><a name="Precedence"></a> Informazioni sulla priorità delle opzioni di visualizzazione  
 Quando si desidera controllare il tipo di visualizzazione di un punto, una linea o un poligono su un livello mappa, è necessario capire dove sia possibile impostare le opzioni di visualizzazione e quali opzioni abbiano una priorità più alta. Le seguenti opzioni di visualizzazione sono elencate a partire da quella con priorità più bassa. Le opzioni di visualizzazione più in alto ignorano le opzioni di visualizzazione riportate più in basso in questo elenco:  
  
-   Opzioni dei livelli.  
  
-   Opzioni Punti, Linee o Poligoni su ogni livello. Queste opzioni si applicano se gli elementi della mappa vengono recuperati in modo dinamico durante l'elaborazione del report o se vengono incorporati nella definizione del report. Ad esempio si specifica un colore di riempimento per tutti gli elementi di un livello.  
  
-   Regole. È possibile impostare regole per controllare il colore, le dimensioni, lo spessore o il tipo di marcatore per tutti gli elementi della mappa di un livello. Le regole che è possibile impostare dipendono dal tipo di elementi della mappa.  
  
    -   Regole colore. Si applicano ai marcatori per punti, linee, poligoni e ai marcatori per i punti centrali dei poligoni.  
  
    -   Regole dimensioni. Si applicano ai marcatori per punti e ai marcatori per i punti centrali dei poligoni.  
  
    -   Regole spessore. Si applicano alle lunghezze righe.  
  
    -   Regole di tipo marcatore. Si applicano ai marcatori per punti e ai marcatori per i punti centrali dei poligoni.  
  
-   Opzioni di sostituzione per singoli punti, linee o poligoni incorporati su un livello. Le modifiche che si apportano sono permanenti. Per ripristinare queste modifiche, è necessario ricaricare i dati per il livello.  
  
 Per altre informazioni, vedere [Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  

  
## <a name="see-also"></a>Vedere anche  
 [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Mappe &#40;Generatore report e SSRS&#41;](maps-report-builder-and-ssrs.md)  
  
  
