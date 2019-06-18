---
title: Rendering degli elementi del report (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 99ebb4dc-41cc-42ac-82dd-a2b0e31155a0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ae3b511031b95023ab8ebe2a8e4c0aa065d4f35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65576448"
---
# <a name="rendering-report-items-report-builder-and-ssrs"></a>Rendering degli elementi del report (Generatore report e SSRS)
  Il numero, le dimensioni e la posizione degli elementi del report influiscono sulla modalità di paginazione del corpo del report da parte dei renderer. Di seguito è riportata una descrizione della modalità di rendering dei vari elementi del report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="overlapping-report-items"></a>Elementi del report sovrapposti  
 Gli elementi del report sovrapposti non sono supportati in HTML, MHTML, Word, Excel, in Anteprima o nel Visualizzatore report. Se esistono, tali elementi vengono spostati. Per gli elementi del report sovrapposti si applicano le regole seguenti:  
  
-   Se la sovrapposizione verticale degli elementi del report è maggiore, uno degli elementi sovrapposti viene spostato a destra. L'elemento all'estrema sinistra rimane dove è posizionato.  
  
-   Se la sovrapposizione orizzontale degli elementi del report è maggiore, uno degli elementi sovrapposti viene spostato verso il basso. L'elemento più in alto rimane dove è posizionato.  
  
-   Se la sovrapposizione verticale è uguale a quella orizzontale, uno degli elementi sovrapposti viene spostato a destra. L'elemento all'estrema sinistra rimane dove è posizionato.  
  
-   Se è necessario spostare un elemento nella sovrapposizione corretta, gli elementi del report adiacenti vengono spostati verso il basso e/o verso destra per mantenere una quantità minima di spaziatura tra l'elemento e gli elementi che terminano sopra di esso e/o alla sua sinistra. Si supponga ad esempio che due elementi si sovrappongano in verticale e che un terzo elemento si trovi alla loro destra a una distanza di 5 centimetri. Quando l'elemento del report sovrapposto viene spostato a destra, anche il terzo elemento si sposta a destra per mantenere la distanza di 5 centimetri con l'elemento a sinistra.  
  
 Gli elementi del report sovrapposti sono supportati nei formati con interruzioni di pagina manuali, inclusa la stampa.  
  
## <a name="visibility-and-report-items"></a>Visibilità ed elementi del report  
 Gli elementi del report possono essere nascosti oppure visualizzati per impostazione predefinita o in base a determinate condizioni tramite espressioni. Facoltativamente, la visibilità può essere disattivata facendo clic su un altro elemento del report.  
  
 Per il rendering degli elementi del report si applicano le regole di visibilità seguenti:  
  
-   Se un elemento del report e il relativo contenuto sono sempre nascosti (ovvero l'elemento non è nascosto in base a un'espressione o la visibilità non può essere disattivata facendo clic su un altro elemento del report), gli altri elementi a destra o sotto di esso non vengono spostati per riempire lo spazio vuoto. Ad esempio, se un rettangolo e l'immagine contenuta al suo interno sono nascosti, l'elemento del report che inizia a destra del rettangolo non viene spostato a sinistra per riempire quello che sembra uno spazio vuoto. Lo spazio occupato dal rettangolo viene mantenuto.  
  
-   Se un elemento del report e il relativo contenuto sono nascosti in base a determinate condizioni (ovvero l'elemento è nascosto in base a un'espressione o la relativa visibilità viene disattivata facendo clic su un altro elemento del report), gli elementi a destra o sotto di esso vengono spostati a sinistra per riempire lo spazio lasciato vuoto dall'elemento nascosto.  
  
-   Se la visibilità di un elemento del report e del relativo contenuto può essere disattivata facendo clic su un altro elemento, la paginazione cambia in base all'elemento del report e al relativo contenuto solo quando questo viene inizialmente visualizzato.  
  
## <a name="keeping-report-items-together-on-a-single-page"></a>Elementi del report mantenuti assieme in un'unica pagina  
 È possibile mantenere assieme molti elementi di un report in una singola pagina in modo implicito o esplicito impostando le proprietà Keep With Group o Keep Together. Il rendering degli elementi del report viene sempre eseguito nella stessa pagina se tali elementi non includono interruzioni di pagina logiche e sono di dimensioni minori rispetto all'area della pagina utilizzabile. Se un elemento del report non rientra completamente nella pagina da cui dovrebbe iniziare, prima di tale elemento viene inserita un'interruzione di pagina manuale per forzarlo alla pagina successiva. Per i renderer di interruzioni di pagine software, le dimensioni della pagina aumentano in base all'elemento del report.  
  
 Quando l'elemento del report è sempre nascosto, le regole per mantenere assieme gli elementi vengono ignorate.  
  
 Gli elementi seguenti vengono sempre mantenuti assieme:  
  
-   Immagini.  
  
-   Linee.  
  
-   Grafici, misuratori e mappe.  
  
-   Singola riga di un'area dati visualizzata separatamente in un'altra pagina, selezionando l'opzione Keep With Group. La singola riga verrà implicitamente mantenuta assieme ad almeno un'istanza del gruppo in modo che non rimanga isolata. È possibile impostare questa opzione in un'area dati o in un gruppo.  
  
-   Area di intestazione di un'area dati.  
  
-   Area di intestazione di un'area dati e prima riga di dati.  
  
-   Elementi del report la cui visualizzazione può essere attivata o disattivata in un'area dati Tablix.  
  
### <a name="priority-order"></a>Ordine di priorità  
 A causa delle limitazioni delle dimensioni della pagina, possono verificarsi conflitti tra le regole per mantenere insieme gli elementi del report. In questo caso, viene utilizzato il seguente ordine di priorità per mantenere assieme gli elementi durante il rendering:  
  
-   Linee, grafici e immagini.  
  
-   Controllo di righe orfane e isolate.  
  
-   Intestazioni di colonna e intestazioni di riga ripetute.  
  
     Le intestazioni hanno la precedenza rispetto ai piè di pagina. I gruppi ripetuti interni hanno la priorità rispetto ai gruppi esterni. Gli elementi con la proprietà **RepeatWith** impostata che si trovano più vicino all'area dati di destinazione hanno la priorità rispetto agli elementi che si trovano a una distanza maggiore.  
  
-   Elementi del report di piccole dimensioni, ad esempio caselle di testo o rettangoli, con la proprietà KeepTogether esplicita impostata su **true**.  
  
-   Elementi del report di grandi dimensioni, ad esempio sottoreport o un membro Tablix diverso da quello più interno, con la proprietà KeepTogether esplicita impostata su **true**.  
  
-   Aree dati Tablix con la proprietà KeepTogether esplicita impostata su **true**.  
  
### <a name="subreports"></a>Sottoreport  
 Un sottoreport viene visualizzato come un rettangolo che contiene un altro report definito in un file rdl di report separato. Il file del sottoreport deve essere pubblicato in un server di report prima che il report padre possa accedervi.  
  
 Per il rendering dei sottoreport si applicano le regole seguenti:  
  
-   Le dimensioni dei sottoreport possono aumentare fino a quelle del corpo definite nel file rdl di definizione del sottoreport. Ad esempio, se nel file RDL del sottoreport è indicato che la larghezza del corpo del sottoreport è pari a 12 centimetri, la larghezza del sottoreport sarà di 12 centimetri all'interno del report padre.  
  
-   I sottoreport ereditano le impostazioni di colonna dal report padre. Le impostazioni di colonna definite nel file RDL originale vengono sempre ignorate.  
  
-   Viene eseguito il rendering solo del corpo del sottoreport. Il rendering delle sezioni di intestazione e piè di pagina definite nel file rdl del sottoreport non viene eseguito durante il rendering del sottoreport nel report padre.  
  
-   I sottoreport hanno una proprietà KeepTogether esplicita. Quando è impostata su **true**, tutti gli elementi del sottoreport vengono mantenuti assieme in un'unica pagina, se possibile.  
  
-   Se non è possibile eseguire un sottoreport, questo viene visualizzato nel report come casella di testo con un messaggio di errore. Le proprietà di stile applicate al sottoreport vengono invece applicate alla casella di testo.  
  
-   Se il sottoreport è diviso da un'interruzione di pagina, l'impostazione **Ometti bordo sull'interruzione di pagina** controlla se i bordi del sottoreport sono chiusi o aperti.  
  
 Per altre informazioni sui sottoreport, vedere [Sottoreport &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
