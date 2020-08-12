---
title: Intestazioni di pagina e piè di pagina (Generatore report) | Microsoft Docs
description: Informazioni sui molti elementi che è possibile aggiungere a intestazioni e piè di pagina, tra cui testo, immagini, rettangoli, bordi, colore di sfondo ed espressioni in Generatore report.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ca788f2b86e2e71465228a7e00cf55efb86c8914
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84778373"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>Intestazioni di pagina e piè di pagina (Generatore report e SSRS)
  Un report può contenere un'intestazione e un piè di pagina, posizionati rispettivamente nella parte superiore e inferiore di ogni pagina. Le intestazioni e i piè di pagina possono contenere testo statico, immagini, linee, rettangoli, bordi, colore di sfondo, immagini di sfondo ed espressioni. Le espressioni includono riferimenti ai campi del set di dati per i report contenenti un solo set di dati e chiamate di funzioni di aggregazione che includono il set di dati come ambito.  
  
> [!NOTE]  
>  Ogni estensione per il rendering elabora le pagine in modo diverso. Per altre informazioni sulle estensioni per il rendering e la paginazione dei report, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Per impostazione predefinita, i report includono piè di pagina, ma non intestazioni di pagina. Per altre informazioni su come aggiungerli o rimuoverli, vedere [Aggiungere o rimuovere un'intestazione o un piè di pagina &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
 Le intestazioni e i piè di pagina contengono in genere numeri di pagina, titoli del report e altre proprietà del report. Per altre informazioni su come aggiungere questi elementi all'intestazione o al piè di pagina, vedere [Visualizzare i numeri di pagina o altre proprietà del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md).  
  
 In seguito alla creazione, l'intestazione o il piè di pagina viene visualizzato in ogni pagina del report. Per altre informazioni sull'esclusione delle intestazioni e dei piè di pagina nella prima e nell'ultima pagina, vedere [Nascondere un'intestazione o un piè di pagina nella prima o nell'ultima pagina &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>Intestazioni e piè di pagina del report  
 Le intestazioni e i piè di pagina delle pagine e dei report sono differenti. I report non dispongono di un'area speciale per le intestazioni o i piè di pagina. L'intestazione di un report è costituita dagli elementi del report posizionati all'inizio del corpo del report nella relativa area di progettazione. Tali elementi vengono visualizzati una sola volta come primo contenuto del report. Il piè di pagina di un report è costituito dagli elementi del report posizionati nella parte inferiore del corpo del report. Tali elementi vengono visualizzati una sola volta come ultimo contenuto del report.  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>Visualizzazione di dati variabili in un'intestazione o in un piè di pagina  
 Le intestazioni e i piè di pagina possono includere contenuto statico, ma vengono più frequentemente utilizzati per visualizzare contenuto variabile, ad esempio numeri di pagina o informazioni sul contenuto di una pagina. Per visualizzare dati variabili diversi per ogni pagina, è necessario specificare un'espressione.  
  
 Se nel report è definito un solo set di dati, è possibile aggiungere espressioni semplici come `[FieldName]` a un'intestazione o a un piè di pagina. Trascinare il campo dalla raccolta di campi del set di dati del riquadro dei dati del report o dalla raccolta Campi predefiniti nell'intestazione o nel piè di pagina. Verrà automaticamente aggiunta una casella di testo con l'espressione appropriata.  
  
 Per calcolare le somme o le altre aggregazioni per i valori nella pagina, è possibile utilizzare espressioni di aggregazione che specificano ReportItems o il nome di un set di dati. La raccolta ReportItems è la raccolta di caselle di testo inclusa in ogni pagina dopo l'esecuzione del rendering del report. Nella definizione del report è necessario che sia presente il nome del set di dati. Nella tabella seguente sono riportati gli elementi supportati in ogni tipo di espressione di aggregazione:  
  
|Elementi supportati nell'espressione|Aggregazioni ReportItems|Aggregazioni Dataset (l'ambito deve essere il nome del set di dati)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|Caselle di testo nel corpo del report|Sì|No|  
|&PageNumber|Sì|No|  
|&TotalPages|Sì|No|  
|Funzione di aggregazione|Sì. Ad esempio,<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|Sì. Ad esempio,<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|Raccolta Fields per gli elementi della pagina|Indirettamente. Ad esempio,<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|Sì. Ad esempio,<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|Immagine con associazione a dati|Indirettamente. Ad esempio, usare `=ReportItems!TXT_Photo.Value`|Sì. Ad esempio,<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 Nelle sezioni seguenti di questo argomento vengono illustrate alcune espressioni già esistenti per il recupero dei dati variabili comunemente utilizzati nelle intestazioni e nei piè di pagina. In una sezione viene inoltre indicato il modo in cui l'estensione per il rendering Excel elabora le intestazioni e i piè di pagina. Per altre informazioni sulle espressioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>Aggiunta dei totali di pagina calcolati a un'intestazione o un piè di pagina  
 Per alcuni report è utile includere nell'intestazione o nel piè di pagina di ogni report un valore calcolato, ad esempio il totale della somma per pagina se la pagina include valori numerici. Poiché non è possibile fare riferimento ai campi direttamente, l'espressione che si inserisce nell'intestazione o nel piè di pagina deve fare riferimento al nome dell'elemento del report, ad esempio una casella di testo, piuttosto che al campo dati:  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 Se la casella di testo si trova in una tabella o in un elenco che contiene righe di dati ripetute, il valore visualizzato nell'intestazione o nel piè di pagina in fase di esecuzione è una somma di tutti i valori di tutti i dati dell'istanza `TextBox1` nella tabella o nell'elenco relativo alla pagina corrente.  
  
 Quando si esegue il calcolo dei totali della pagina, si potrebbero notare differenze nei totali quando si utilizzano estensioni per il rendering diverse per visualizzare il report. L'output impaginato viene calcolato in maniera diversa per ogni estensione per il rendering. La stessa pagina visualizzata in formato HTML potrebbe indicare totali diversi quando viene visualizzata in formato PDF, se il totale dei dati nella pagina PDF è diverso. Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="for-reports-with-multiple-datasets"></a>Per i report con più set di dati  
 Per i report con più set di dati, non è possibile aggiungere direttamente campi o immagini con associazione a dati a un'intestazione o un piè di pagina. È tuttavia possibile scrivere un'espressione che faccia indirettamente riferimento a un campo o un'immagine con associazione a dati che si desidera utilizzare in un'intestazione o in un piè di pagina.  
  
 Per inserire dati variabili in un'intestazione o in un piè di pagina, eseguire la procedura seguente:  
  
-   Aggiungere una casella di testo all'intestazione o al piè di pagina.  
  
-   Nella casella di testo scrivere un'espressione che genera i dati variabili che si desidera visualizzare.  
  
-   Nell'espressione includere i riferimenti agli elementi del report nella pagina. È possibile ad esempio fare riferimento a una casella di testo che contiene i dati provenienti da un determinato campo. Non includere un riferimento diretto ai campi in un set di dati. Non è possibile ad esempio usare l'espressione `[LastName]`. È invece possibile utilizzare l'espressione seguente per visualizzare il contenuto della prima istanza di una casella di testo denominata `TXT_LastName`:  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 Non è possibile utilizzare funzioni di aggregazione per i campi presenti nell'intestazione o nel piè di pagina. È consentita solo la specifica di una funzione di aggregazione sugli elementi del report contenuti nel corpo del report. Per le espressioni comuni nelle intestazioni e nei piè di pagina, vedere [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>Aggiunta di un'immagine con associazione a dati a un'intestazione o un piè di pagina  
 In un'intestazione o in un piè di pagina è possibile utilizzare i dati delle immagini archiviati in un database. Non è tuttavia possibile fare riferimento ai campi di un database direttamente da un elemento del report Immagine. È invece necessario aggiungere una casella di testo al corpo del report e quindi impostare tale casella sul campo dati che contiene l'immagine. Si noti che il valore deve avere la codifica Base64. È possibile nascondere la casella di testo nel corpo del report per evitare di visualizzare l'immagine con codifica Base64. È quindi possibile fare riferimento al valore della casella di testo nascosta tramite l'elemento del report Immagine nell'intestazione o nel piè di pagina.  
  
 Si supponga ad esempio che un report sia costituito da pagine di informazioni sul prodotto e che si desideri visualizzare una fotografia del prodotto nell'intestazione di ogni pagina. Per stampare un'immagine archiviata nell'intestazione del report, definire una casella di testo nascosta denominata `TXT_Photo` nel corpo del report che recupera l'immagine dal database e usa un'espressione per attribuirle un valore:  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 Nell'intestazione aggiungere un elemento del report Immagine che usa la casella di testo `TXT_Photo` decodificata per visualizzare l'immagine:  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>Utilizzo di intestazioni e piè di pagina per posizionare il testo  
 È possibile utilizzare le intestazioni e i piè di pagina per posizionare il testo in una pagina. Si supponga ad esempio di voler creare un report da inviare ai clienti. È possibile utilizzare l'intestazione o il piè di pagina per posizionare l'indirizzo del cliente in modo che sia visibile dalla finestra una volta inserito nella busta.  
  
 Se si utilizza la casella di testo solo per popolare un'intestazione o un piè di pagina, è possibile nasconderla nel corpo del report. La posizione della casella di testo nel corpo del report può determinare se il valore viene visualizzato nell'intestazione o nel piè di pagina della prima o dell'ultima pagina di un report. Se ad esempio vi sono tabelle, matrici o elenchi che determinano l'estensione del report su più pagine, il valore della casella di testo nascosta viene visualizzato nell'ultima pagina. Se si desidera visualizzare tale valore nella prima pagina, posizionare la casella di testo nascosta nella parte superiore del corpo del report.  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>Progettazione di report con intestazioni e piè di pagina per renderer specifici  
 Durante l'elaborazione di un report, le informazioni sui relativi dati ed elementi di layout vengono combinate. Quando si visualizza un report, le informazioni combinate vengono passate a un renderer che determina la quantità di dati che è possibile inserire in ogni pagina del report.  
  
 Se si visualizza un report sul server di report utilizzando un browser, il renderer HTML controlla il contenuto nelle pagine del report visualizzate. Se si intende recapitare i report in un formato diverso da quello utilizzato per la visualizzazione o si intende stampare i report in un formato specifico, potrebbe essere necessario ottimizzare il layout del report per il renderer che verrà utilizzato per il formato del report finale. Per altre informazioni sulla paginazione dei report, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Utilizzo delle intestazioni e dei piè di pagina in Excel  
 Per ottenere risultati migliori quando si definiscono le intestazioni e i piè di pagina per i report che utilizzano l'estensione per il rendering Excel, attenersi alle linee guida seguenti:  
  
-   Utilizzare i piè di pagina per visualizzare i numeri di pagina.  
  
-   Utilizzare le intestazioni di pagina per visualizzare immagini, titoli o altro testo. Non inserire i numeri di pagina nell'intestazione di pagina.  
  
 In Excel i piè di pagina hanno un layout limitato. Se si definisce un report che include elementi complessi del report all'interno del piè di pagina, quest'ultimo non verrà eseguito come previsto quando il report viene visualizzato in formato Excel.  
  
 L'estensione per il rendering Excel consente di adattare le immagini e il posizionamento assoluto di elementi semplici o complessi del report nell'intestazione di pagina. Un effetto collaterale del supporto di un layout più completo per l'intestazione di pagina è rappresentato da un supporto ridotto per il calcolo dei numeri di pagina nell'intestazione. Nell'estensione per il rendering Excel le impostazioni predefinite determinano il calcolo dei numeri di pagina in base al numero dei fogli di lavoro. In base a come viene definito il report, questo potrebbe dare luogo a numeri di pagina errati. Si supponga ad esempio che un report venga visualizzato come un singolo, grande foglio di lavoro stampato su quattro pagine. Se si includono le informazioni relative al numero di pagina nell'intestazione di pagina, nell'intestazione di ogni pagina stampata verrà visualizzata la scritta "Pagina 1 di 1".  
  
 Per un calcolo più preciso delle pagine ci si basa sulle pagine logiche correlate alle dimensioni di una pagina stampata. Nel piè di pagina di Excel viene utilizzato automaticamente il numero di pagine logiche. Per inserire il conteggio delle pagine logiche nell'intestazione di pagina, è necessario configurare le impostazioni per le informazioni sul dispositivo sull'utilizzo di intestazioni semplici. Si tenga presente che quando si utilizzano intestazioni semplici, non è più possibile gestire layout di report complessi nell'area dell'intestazione.  
  
 Per altre informazioni, vedere [Esportazione in Microsoft Excel &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Incorporare un'immagine in un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Rettangoli e linee &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
