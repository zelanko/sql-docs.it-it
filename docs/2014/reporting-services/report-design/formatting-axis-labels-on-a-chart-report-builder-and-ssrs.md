---
title: Formattazione delle etichette degli assi in un grafico (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10148"
- sql12.rtp.rptdesigner.calculatedseriesproperties.axeschartareas.f1
- "10142"
- sql12.rtp.rptdesigner.axisproperties.minortickmarks.f1
- "10143"
- sql12.rtp.rptdesigner.axisproperties.labels.f1
- "10145"
- sql12.rtp.rptdesigner.axistitleproperties.font.f1
- "10139"
- sql12.rtp.rptdesigner.axisproperties.labelfont.f1
- "10140"
- sql12.rtp.rptdesigner.axisproperties.majortickmarks.f1
- sql12.rtp.rptdesigner.axisproperties.line.f1
- "10141"
helpviewer_keywords:
- "10140"
ms.assetid: ddf50dd5-5314-42ff-97f4-c3a4a17cfcdd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a98a3496e237de1d4eeb530dfe5e22b70149890
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105849"
---
# <a name="formatting-axis-labels-on-a-chart-report-builder-and-ssrs"></a>Formattazione delle etichette degli assi in un grafico (Generatore report e SSRS)
  Nei tipi di grafico basati su coordinate (grafico a barre, ad area, a punti, a linee, con intervalli e istogramma) sono inclusi due assi utilizzati per la classificazione e la visualizzazione di relazioni tra dati. A ogni asse verranno applicati tipi diversi di formattazione.  
  
 È possibile formattare gli assi usando la finestra di dialogo **Proprietà asse** o il riquadro Proprietà. Fare clic con il pulsante destro del mouse sull'asse che si desidera formattare, quindi scegliere **Proprietà asse** per modificare i valori relativi al testo, i formati numerici e di data, i segni di graduazione principali e secondari, l'adattamento automatico per le etichette, nonché lo spessore, il colore e lo stile della linea dell'asse. Per modificare valori per il titolo dell'asse, fare clic con il pulsante destro del mouse sul titolo dell'asse, quindi scegliere **Proprietà titolo asse**.  
  
 Le etichette di un asse identificano gli intervalli principali nel grafico. Per impostazione predefinita, viene utilizzato un algoritmo per determinare il posizionamento ottimale delle etichette sull'asse del grafico ed evitare la sovrapposizione di testo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="types-of-axes"></a>Tipi di assi  
 Il grafico include due assi principali: l'asse dei valori e l'asse delle categorie.  
  
 ![Asse dei valori e asse delle categorie del grafico](../media/rsaxes-categorical-vs-value.gif "Asse dei valori e asse delle categorie del grafico")  
  
 Quando si trascina un campo dal set di dati alla superficie del grafico, verrà determinato se tale campo appartiene all'asse delle categorie o dei valori.  
  
 L'asse dei valori è in genere l'asse verticale del grafico, ovvero l'asse Y. Viene utilizzato per visualizzare i valori di dati numerici da tracciare. Un campo trascinato nell'area dei campi dati verrà tracciato sull'asse dei valori. L'asse delle categorie è in genere l'asse orizzontale del grafico, ovvero l'asse X. Per i grafici a barre, questi assi sono invertiti. Nei tipi di grafico a barre, infatti, l'asse delle categorie corrisponde all'asse verticale, mentre l'asse dei valori a quello orizzontale. Per altre informazioni, vedere [Grafici a barre &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
## <a name="how-the-chart-calculates-axis-label-intervals"></a>Calcolo degli intervalli delle etichette degli assi  
 Prima di formattare le etichette degli assi, è necessario comprendere in che modo vengono calcolati i relativi intervalli. In questo modo sarà possibile impostare le proprietà necessarie per ottenere il comportamento desiderato per le etichette degli assi.  
  
 La scala dell'asse è associata a un valore minimo e a un valore massimo che definiscono l'intervallo dei dati da visualizzare lungo l'asse. Questi valori minimo e massimo vengono calcolati lungo ogni asse in base ai valori del set di risultati. Sull'asse dei valori la scala verrà sempre determinata dal numero minimo e massimo nel campo valori. Sull'asse delle categorie i tipi di valori minimo e massimo vengono determinati in base al tipo del campo categoria. I campi di un set di dati possono essere classificati in uno di tre tipi di campo categoria disponibili, illustrati nella tabella seguente.  
  
|Tipo di campo categoria|Descrizione|Esempio|  
|-------------------------|-----------------|-------------|  
|Numeric|Le categorie vengono tracciate in ordine numerico lungo l'asse X.|In un report sulle vendite basato sul numero di identificazione del dipendente vengono visualizzati i numeri di identificazione dei dipendenti lungo l'asse X.|  
|Data/ora|Le categorie vengono tracciate in ordine cronologico lungo l'asse X.|In un report sulle vendite basato sul mese vengono visualizzate le date formattate lungo l'asse X.|  
|Stringhe|Le categorie vengono tracciate nell'ordine in cui appaiono per la prima volta nell'origine dati lungo l'asse X.|In un report sulle vendite basato sull'area geografica vengono visualizzati i nomi delle aree geografiche lungo l'asse X.|  
  
 Tutti i tipi di grafico con due assi sono progettati per eliminare alcune etichette degli assi quando le categorie sono troppo numerose per rientrare nello spazio disponibile, in modo da produrre un'immagine più chiara sul grafico ed evitare la sovrapposizione delle etichette.  
  
 L'applicazione calcola il punto in cui vengono posizionate le etichette su un asse in base ai passaggi seguenti:  
  
1.  Vengono identificati i valori minimo e massimo in base ai valori nel set di risultati.  
  
2.  Viene calcolato un numero di intervalli equidistanti dell'asse, in genere compreso tra quattro e sei, in base a questi valori minimo e massimo.  
  
3.  Le etichette degli assi vengono visualizzate in base alle relative proprietà, in corrispondenza di tali intervalli. Le proprietà che influiscono sulla posizione delle etichette includono le dimensioni del carattere, l'angolo di visualizzazione delle etichette e le proprietà di ritorno a capo del testo. Queste opzioni di adattamento delle etichette degli assi possono essere modificate.  
  
### <a name="example-of-how-the-chart-calculates-axis-labels"></a>Esempio di calcolo delle etichette degli assi  
 La tabella seguente contiene esempi di dati sulle vendite da tracciare in un istogramma. Il campo Name viene aggiunto all'area Gruppi di categorie e il campo Quantity all'area Valori.  
  
|nome|Quantity|  
|----------|--------------|  
|Michael Blythe|229|  
|Jae Pak|112|  
|Ranjit Varkey Chudukatil|494|  
|Jillian Carson|247|  
|Linda Mitchell|339|  
|Rachel Valdez|194|  
  
 Il campo Quantity viene tracciato lungo l'asse dei valori. Il valore minimo è 112, mentre il valore massimo è 494. In questo caso, la scala viene calcolata per iniziare in corrispondenza di 0 e terminare in corrispondenza di 500. Vengono inoltre calcolati cinque intervalli equidistanti di 100 e vengono create etichette in corrispondenza dei punti 0, 100, 200, 300, 400 e 500.  
  
 Il campo Name viene tracciato lungo l'asse delle categorie. Viene calcolato un numero di etichette compreso tra quattro e sei e vengono determinate le impostazioni di adattamento automatico delle etichette sull'asse delle categorie in modo da evitare la sovrapposizione. Di conseguenza, è possibile che alcune etichette delle categorie vengano omesse. È possibile ignorare le opzioni di adattamento in modo indipendente per ogni asse.  
  
## <a name="displaying-all-labels-on-the-category-axis"></a>Visualizzazione di tutte le etichette sull'asse delle categorie.  
 Sull'asse dei valori gli intervalli forniscono una misura coerente dei punti dati del grafico. Sull'asse delle categorie è tuttavia possibile che tale funzionalità provochi la visualizzazione delle categorie senza etichette. In genere, si desidera che tutte le categorie siano identificate da etichette. È possibile impostare il numero di intervalli su 1 per visualizzare tutte le categorie.  Per altre informazioni, vedere [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Se si sostituiscono le caratteristiche di assegnazione automatica di etichette con un intervallo manuale su un asse, è necessario che tutti gli altri elementi del grafico vengano ridimensionati in modo appropriato. Di conseguenza, è possibile che si ottengano risultati imprevisti per il ridimensionamento e il posizionamento delle etichette o per le dimensioni di altri elementi del grafico.  
  
## <a name="variable-axis-intervals"></a>Intervalli variabili degli assi  
 Nel grafico vengono calcolati circa cinque intervalli di etichette degli assi indipendentemente dalle dimensioni del grafico stesso. Nei grafici di larghezza o di altezza maggiore, se vengono visualizzate solo cinque etichette su un asse, tra un'etichetta e l'altra etichetta appaiono gap più ampi. In questo modo diventa più difficile identificare il valore di ogni punto dati rispetto all'asse. Per evitare questo comportamento nei grafici con tali caratteristiche, è possibile impostare un intervallo variabile degli assi. Verrà calcolato il numero ottimale di etichette che è possibile visualizzare sull'asse in base alla larghezza o all'altezza del grafico, a seconda dell'asse corrispondente. Per altre informazioni, vedere [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md).  
  
## <a name="sorting-axis-values"></a>Ordinamento dei valori degli assi  
 Le categorie vengono visualizzate lungo l'asse X nell'ordine in cui appaiono nel set di risultati. È possibile modificare l'ordine di raggruppamento aggiungendo un comando SORT alla query oppure ordinando il set di dati tramite un'espressione. Le aree dati del grafico vengono ordinate allo stesso modo di tutte le altre aree dati. Per altre informazioni su come ordinare i dati, vedere [Ordinare i dati in un'area dati &#40;Generatore report e SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="specifying-scalar-values-on-the-category-axis"></a>Specifica di valori scalari sull'asse delle categorie  
 Per impostazione predefinita, le etichette degli assi verranno visualizzate nel grafico solo per i punti dati del set di dati che contengono valori validi. Ad esempio, se sull'asse delle categorie sono riportati i valori 1, 2 e 6, nel grafico verranno visualizzate solo le categorie 1, 2 e 6. Per mantenere la scala di valori delle categorie, è possibile specificare l'utilizzo di un asse scalare. In questo caso, verranno visualizzate le etichette relative a 1-6 sull'asse X del grafico, anche se il set di dati non contiene valori per 3-5.  
  
 È possibile impostare un asse scalare in due modi:  
  
-   Selezionare l'opzione **Asse scalare** nella finestra di dialogo **Proprietà asse** . Verranno aggiunti valori numerici o di tipo data/ora all'asse laddove non esistono valori di raggruppamento dati. Per altre informazioni, vedere [Finestra di dialogo Proprietà asse, Opzioni asse &#40;Generatore report e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md).  
  
-   Selezionare un campo o digitare un'espressione per l'opzione **Campo categoria** nella finestra di dialogo **Proprietà serie** . Verranno aggiunti intervalli dell'asse per tutti i valori nel campo categoria specificato.  
  
## <a name="adding-or-removing-side-margins-from-the-category-axis"></a>Aggiunta o rimozione di margini laterali dall'asse delle categorie  
 Nei tipi di grafico a barre, istogramma e a dispersione vengono automaticamente aggiunti margini laterali alle estremità dell'asse X. Non è possibile modificare le dimensioni del margine. In tutti gli altri tipi di grafico non vengono aggiunti margini laterali. Per altre informazioni, vedere [Aggiungere o rimuovere i margini da un grafico &#40;Generatore report e SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)  
  
 [Posizionamento di etichette in un grafico &#40;Generatore report e SSRS&#41;](position-labels-in-a-chart-report-builder-and-ssrs.md)  
  
 [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [Aggiungere o rimuovere i margini da un grafico &#40;Generatore report e SSRS&#41;](add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [Specificare una scala logaritmica &#40;Generatore report e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
