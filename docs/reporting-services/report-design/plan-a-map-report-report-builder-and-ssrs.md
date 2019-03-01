---
title: Pianificare un report mappa (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d7a744233ace7e6c31bb2d00c5bdd888a4be371f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288049"
---
# <a name="plan-a-map-report-report-builder-and-ssrs"></a>Pianificare un report mappa (Generatore report e SSRS)
Report validi presentano informazioni che consentono una migliore comprensione e determinano azioni specifiche. Per presentare dati analitici, come i totali delle vendite o i dati demografici, rispetto a un contesto geografico, è possibile aggiungere una mappa al report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Una mappa può contenere più livelli, in ciascuno dei quali vengono visualizzati elementi della mappa definiti da un tipo specifico di dati spaziali, ossia punti che rappresentano posizioni, linee che rappresentano percorsi o poligoni che rappresentano aree. È possibile associare i dati analitici agli elementi della mappa su ogni livello.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> Specificare lo scopo della mappa  
 Una buona progettazione di report offre informazioni che facilitano la scelta delle azioni da intraprendere da parte degli utenti per la soluzione dei problemi. Per creare una vista mappa che sia utile e facilmente comprensibile, decidere per quali esigenze la mappa offrirà un supporto. Su una mappa è possibile visualizzare, ad esempio, i seguenti tipi di dati per identificare le opportunità del mercato:  
  
-   Vendite relative per ogni negozio.  
  
-   Vendite suddivise in categorie per dati demografici del cliente, in base alla posizione del cliente relativamente all'ubicazione dei negozi.  
  
-   Vendite comparate o altri dati finanziari per territorio di vendita.  
  
-   Vendite comparate per strategie di sconto differenti tra più negozi.  
  
 Dopo aver identificato lo scopo della vista mappa, è necessario analizzare i dati necessari. I dati analitici provengono dai set di dati del report. I dati relativi alla posizione provengono dalle origini dei dati spaziali che è necessario specificare.  
  
##  <a name="Data"></a> Specificare i dati spaziali e quelli analitici  
 L'utente deve specificare i dati spaziali e analitici necessari.  
  
 I dati analitici provengono da un set di dati del report, da dati di esempio inclusi in una mappa della raccolta mappe o da dati analitici inclusi nei dati spaziali in un file di forma ESRI.  
  
 I dati spaziali sono disponibili in tre forme: punti, linee e poligoni.  
  
-   **Punti.** I punti specificano posizioni, ad esempio una città o l'indirizzo di un negozio, di un ristorante o di un centro riunioni. Per ogni posizione che si desidera visualizzare su una mappa, è necessario fornire i dati spaziali relativi a quella posizione. Dopo aver aggiunto punti a una mappa, è possibile visualizzare un marcatore nella posizione punto e variare il tipo, le dimensioni e il colore del marcatore.  
  
-   **Linee.** Le linee specificano percorsi o itinerari, ad esempio gli itinerari di recapito o i percorsi di volo. Dopo aver aggiunto una linea a una mappa, è possibile variare il colore e lo spessore della linea.  
  
-   **Poligoni.** I poligoni specificano zone, ad esempio aree, territori, paesi, stati, province, regioni, città o zone che includono città, codici postali, prefissi telefonici o aree di censimento. Dopo aver aggiunto poligoni a una mappa, oltre alla struttura, è possibile visualizzare anche un marcatore al centro dell'area del poligono.  
  
 Dopo aver identificato i dati spaziali necessari, occorre trovare un'origine per tali dati.  
  
### <a name="find-a-source-for-spatial-data"></a>Trovare un'origine per i dati spaziali  
 Per trovare i dati spaziali da inserire nella mappa, è possibile utilizzare le origini seguenti:  
  
-   File di forma ESRI, compresi i file di forma disponibili pubblicamente che è possibile cercare su Internet.  
  
-   Dati spaziali provenienti dalle origini dati spaziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Mappe dai report nella raccolta mappe.  
  
-   Siti di terze parti che offrono dati spaziali come file di forma ESRI o dati spaziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Tessere mappa di Bing che forniscono uno sfondo per la vista mappa. Per visualizzare le sezioni in una mappa, è necessario configurare il server di report per supportare i servizi Web di Bing Maps.  
  
 Per ulteriori informazioni, vedere "Dove è possibile ottenere i file di forma ESRI?" in [ Creazione guidata mappa e Creazione guidata livello mappa (Generatore report e SSRS) &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 I dati spaziali possono essere politicamente riservati e forse protetti da copyright. Verificare le condizioni per l'utilizzo e le informative sulla privacy relative alle origine dati spaziali per comprendere la modalità di utilizzo di tali dati nel report.  
  
 Dopo aver trovato i dati desiderati, è possibile incorporarli nella definizione del report o recuperarli dinamicamente durante l'elaborazione del report. Per ulteriori informazioni, vedere [Raggiungere un equilibrio tra le dimensioni della definizione del report e il tempo di elaborazione del report](#Embedding) più avanti in questo argomento.  
  
### <a name="determine-the-spatial-data-and-the-spatial-data-match-fields"></a>Determinare i dati spaziali e i campi delle corrispondenze di tali dati  
 Per visualizzare i dati analitici su una mappa e per variare le dimensioni, il colore o il tipo di marcatore, è necessario specificare i campi che correlano i dati spaziali e quelli analitici.  
  
 I dati spaziali devono contenere i campi seguenti:  
  
-   **Spatial data.** Campo dati spaziali che dispone dei set di coordinate che definiscono ogni punto, linea o poligono.  
  
-   **Campi delle corrispondenze.** Uno o più campi che identificano in modo univoco ogni campo dati spaziali. Ad esempio per il punto relativo alla posizione di un negozio, è possibile utilizzare il nome del negozio. Se questo nome non è univoco nei dati spaziali, è possibile includere il nome della città, oltre a quello del negozio.  
  
 I campi delle corrispondenze sono utilizzati per correlare i dati spaziali con quelli analitici.  
  
### <a name="determine-the-analytical-data-and-the-analytical-data-match-fields"></a>Determinare i dati analitici e i campi delle corrispondenze di tali dati  
 Dopo aver identificato i dati spaziali, è necessario eseguire la stessa operazione con quelli analitici. I dati analitici possono provenire dalle seguenti origini:  
  
-   Set di dati di un report esistente. I campi vengono specificati come semplici espressioni relative a campi, ad esempio [Sales] o = Fields!Sales.Value.  
  
-   Campi dati forniti dall'origine dati spaziali. I campi vengono specificati come parole chiave che iniziano con # seguito dal nome del campo dell'origine dei dati spaziali.  
  
 È necessario quindi determinare i nomi dei campi delle corrispondenze:  
  
-   Campi delle corrispondenze. Uno o più campi che specificano le stesse informazioni dei campi delle corrispondenze dei dati spaziali per compilare una relazione tra i dati spaziali e quelli analitici. Questi campi devono avere lo stesso tipo di dati e la stessa formattazione.  
  
 Una volta identificati l'origine dati spaziali, i dati spaziali, l'origine dati analitici, i dati analitici e i campi delle corrispondenze, è possibile decidere quale tipo di mappa aggiungere al report.  
  
##  <a name="MapType"></a> Scegliere un tipo di mappa  
 Quando si esegue la Creazione guidata mappa, si aggiunge una mappa e il relativo primo livello al report. La procedura guidata consente di aggiungere uno dei seguenti tipi di mappe al report:  
  
-   Mappa di base che visualizza le posizioni senza dati analitici associati.  
  
-   Mappa che dispone di un valore analitico associato a ogni elemento della mappa, ad esempio il totale delle vendite di ogni negozio.  
  
-   Mappa che dispone di più valori analitici associati a un elemento della mappa, ad esempio il numero di clienti e il totale delle vendite di ogni negozio.  
  
 Nella tabella seguente viene descritto ogni tipo di mappa. Tutti i tipi di mappa consentono di selezionare un tema che controlla la tavolozza, lo stile del bordo e il carattere, nonché di visualizzare le etichette.  
  
|Icona della procedura guidata|Stile del livello|Tipo di livello|Descrizione e opzioni|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../../reporting-services/report-design/media/rs-maptype-polygon-basic.gif "rs_MapType_Polygon_Basic")|Mappa di base|Polygon|Mappa che visualizza solo le aree, ad esempio i territori di vendita.<br /><br /> Opzioni: variazione del colore mediante la tavolozza o utilizzo di un solo colore. Una tavolozza è un set predefinito di colori. Una volta assegnati tutti i colori di una tavolozza, vengono assegnate anche le sfumature.|  
|![rs_MapType_Polygon_ColorAnalytical](../../reporting-services/report-design/media/rs-maptype-polygon-coloranalytical.gif "rs_MapType_Polygon_ColorAnalytical")|Mappa analitica a colori|Polygon|Mappa che visualizza i dati analitici variando il colore, ad esempio i dati di vendita per area.|  
|![rs_MapType_Polygon_Bubble](../../reporting-services/report-design/media/rs-maptype-polygon-bubble.gif "rs_MapType_Polygon_Bubble")|Mappa a bolle|Polygon|Mappa che visualizza i dati analitici variando le dimensioni delle bolle al centro delle aree, ad esempio i dati di vendita per area.<br /><br /> Opzioni: variazione dei colori dell'area in base a un secondo campo analitico e indicazione delle regole colore.|  
|![rs_MapType_Line_Basic](../../reporting-services/report-design/media/rs-maptype-line-basic.gif "rs_MapType_Line_Basic")|Mappa linea di base|Riga|Mappa che visualizza solo le linee, ad esempio gli itinerari di recapito.<br /><br /> Opzioni: variazione del colore mediante la tavolozza o utilizzo di un solo colore.|  
|![rs_MapType_Line_Analytical](../../reporting-services/report-design/media/rs-maptype-line-analytical.gif "rs_MapType_Line_Analytical")|Mappa linea analitica|Riga|Mappa che varia il colore e lo spessore della linea, ad esempio il numero di pacchetti recapitati e le metriche di puntualità per itinerari.<br /><br /> Opzioni: variazione dello spessore della linea in base a un campo analitico, variazione del colore della linea in base a un secondo campo analitico e indicazione delle regole colore.|  
|![rs_MapType_Marker_Basic](../../reporting-services/report-design/media/rs-maptype-marker-basic.gif "rs_MapType_Marker_Basic")|Mappa con marcatori di base|Punto|Mappa che visualizza un marcatore per ogni posizione, ad esempio le città.<br /><br /> Opzioni: variazione del colore mediante la tavolozza o utilizzo di un solo colore e modifica dello stile del marcatore.|  
|![rs_MapType_Marker_Bubble](../../reporting-services/report-design/media/rs-maptype-marker-bubble.gif "rs_MapType_Marker_Bubble")|Mappa con marcatori a bolle|Punto|Mappa che visualizza una bolla per ogni posizione e varia le dimensioni della bolla in base a un campo dati analitici, ad esempio i dati di vendita per città.<br /><br /> Opzioni: variazione del colore della bolla in base a un secondo campo analitico e indicazione delle regole colore.|  
|![rs_MapType_Marker_Analytical](../../reporting-services/report-design/media/rs-maptype-marker-analytical.gif "rs_MapType_Marker_Analytical")|Mappa con marcatori analitici|Punto|Mappa che visualizza un marcatore per ogni posizione e varia il colore, le dimensioni e il tipo di marcatore in base ai dati analitici, ad esempio prodotti più venduti, margini di profitto e strategie di sconto.<br /><br /> Opzioni: variazione del tipo di marcatore in base a un campo analitico, variazione delle dimensioni del marcatore in base a un secondo campo analitico, variazione del colore del marcatore in base a un terzo campo analitico e indicazione delle regole colore.|  
  
 Dopo aver aggiunto una mappa con la Creazione guidata mappa, è possibile creare livelli aggiuntivi o modificare le opzioni di un livello tramite la Creazione guidata livello. Per altre informazioni sulle procedure guidate, vedere [Creazione guidata mappa e Creazione guidata livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 È possibile personalizzare la visualizzazione o le opzioni dei dati per ogni livello in modo indipendente. Per altre informazioni sulla personalizzazione di una mappa dopo l'esecuzione di una procedura guidata, vedere [Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="Legend"></a> Pianificare le legende  
 Per facilitare l'interpretazione di una mappa da parte degli utenti, è possibile aggiungere più legende di mappa, una scala dei colori e una scala distanza. Quando si progetta una mappa, stabilire il punto in cui si desidera visualizzare le legende. Per ognuna di esse è possibile specificare le informazioni seguenti:  
  
-   **Posizione della legenda.** Le legende possono essere visualizzate, ad esempio, all'interno o all'esterno del viewport e in 12 posizioni specifiche relative al viewport.  
  
-   **Stili della legenda**. Ad esempio è possibile specificare lo stile del carattere e del bordo, la linea di separazione e le proprietà di riempimento.  
  
-   **Titolo della legenda.** Ad esempio è possibile specificare il testo del titolo e controllare, in modo indipendente, se visualizzare il titolo per una legenda di mappa o la scala dei colori.  
  
-   **Layout della legenda di mappa.** Ad esempio le legende di mappa possono essere visualizzate come tabelle estese in altezza o in larghezza.  
  
 Il contenuto della legenda viene creato automaticamente durante l'elaborazione del report in base alle opzioni regola impostate per ogni livello.  
  
 Per impostazione predefinita, tutti i livelli visualizzano i risultati delle regole nella prima legenda di mappa. È possibile creare più legende e quindi, per ogni regola, decidere quale legenda utilizzare per visualizzare i risultati.  
  
 Per altre informazioni, vedere [Variare la visualizzazione di poligoni, linee e punti in base a regole e dati analitici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md) e [Modificare legende della mappa, scala dei colori e regole associate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
##  <a name="Embedding"></a> Raggiungere un equilibrio tra le dimensioni della definizione del report e il tempo di elaborazione del report  
 Una buona progettazione di report per le mappe richiede un equilibrio tra le opzioni che controllano le prestazioni del report e le dimensioni della definizione del report. Gli elementi della mappa basati sui dati spaziali o le tessere mappa di Bing possono essere statici e incorporati nella definizione del report oppure dinamici e creati ogni volta che viene elaborato il report. È necessario valutare le eventuali conseguenze per i dati della mappa statici o dinamici e trovare l'equilibrio migliore in base alle circostanze. Per prendere tale decisione, considerare le informazioni seguenti:  
  
-   Gli elementi della mappa incorporati possono aumentare notevolmente le dimensioni della definizione del report, ma riducono il tempo necessario per visualizzare la mappa nel report. Il server di report potrebbe avere dei limiti riguardanti le dimensioni a cui è necessario attenersi.  
  
-   La definizione del report specifica i limiti relativi al numero di punti dati spaziali che può essere elaborato e un valore distinto che specifica il numero di elementi della mappa che può essere incluso nella definizione del report.  
  
-   Gli elementi dinamici della mappa riducono le dimensioni della definizione del report, ma aumentano il tempo necessario per elaborare ed eseguire il rendering della mappa.  
  
-   Se l'origine dei dati spaziali si trova nel computer dell'utente, gli elementi della mappa sono sempre incorporati nella definizione del report. Sono inclusi i dati spaziali della raccolta mappe o i file di forma ESRI installati localmente.  
  
 Per utilizzare i dati spaziali dinamici, l'origine dei dati spaziali deve trovarsi sul server di report. Quando i report vengono progettati in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], le origini dati spaziali possono essere aggiunte a un progetto e pubblicate sul server di report insieme alla definizione del report. Se per progettare i report si utilizza Generatore report, è necessario innanzitutto caricare i dati spaziali sul server di report, quindi specificare tale origine dei dati spaziali per il livello mappa nella procedura guidata o nelle proprietà del livello mappa.  
  
## <a name="see-also"></a>Vedere anche  
 [Personalizzare i dati e la visualizzazione di una mappa o di un livello mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Esercitazione: Report mappa &#40;Generatore report&#41;](../../reporting-services/tutorial-map-report-report-builder.md)   
 [Mappe &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Risolvere problemi relativi ai report: Report mappa &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
