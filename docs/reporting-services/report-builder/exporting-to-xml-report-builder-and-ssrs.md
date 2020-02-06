---
title: Esportazione in XML (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 52d83c17a1cfe79f8add7f0764216d404c14cfd9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580752"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>Esportazione in XML (Generatore report e SSRS)
  L'estensione per il rendering XML restituisce un report impaginato in formato XML. Lo schema per il report XML è specifico del report e contiene solo dati. Il rendering delle informazioni di layout non viene eseguito e la paginazione non viene mantenuta dall'estensione per il rendering XML. Il codice XML generato da questa estensione può essere importato in un database, usato come messaggio di dati XML o inviato a un'applicazione personalizzata.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> Elementi del report  
 Nella tabella seguente viene descritto il rendering degli elementi del report.  
  
|Elemento|Tipo di rendering|  
|----------|------------------------|  
|Report|Come elemento di livello principale del documento XML.|  
|Aree dati|Come elemento all'interno dell'elemento del relativo contenitore. Nelle aree dati sono inclusi tabelle, matrici ed elenchi in cui i dati vengono visualizzati sotto forma di testo e grafico, nonché barre dei dati, grafici sparkline, misuratori e indicatori in cui vengono visualizzati dati.|  
|Sezioni dettagli e gruppo|Come elemento, per ogni istanza, all'interno dell'elemento del relativo contenitore.|  
|Casella di testo|Come attributo o elemento all'interno del relativo contenitore.|  
|Rectangle|Come elemento all'interno del relativo contenitore.|  
|Gruppi di colonne della matrice|Come elementi all'interno di gruppi di riga.|  
|Mappa|Come elemento all'interno dell'elemento del relativo contenitore. I livelli mappa sono elementi figlio della mappa e ogni livello mappa include elementi per i relativi membri della mappa e per gli attributi dei membri della mappa.|  
|Grafico|Come elemento all'interno dell'elemento del relativo contenitore. Le serie sono elementi figlio del grafico, mentre le categorie sono elementi figlio di una serie. Viene eseguito il rendering di tutte le etichette del grafico per ogni valore del grafico. Le etichette e i valori sono inclusi come attributi.|  
|Barra dei dati|Come elemento all'interno dell'elemento del relativo contenitore, in modo simile a un grafico. In genere, in una barra dei dati non sono incluse gerarchie o etichette, bensì solo valori.|  
|Grafico sparkline|Come elemento all'interno dell'elemento del relativo contenitore, in modo simile a un grafico. In genere, in un grafico sparkline non sono incluse gerarchie o etichette, bensì solo valori.|  
|Misuratore|Come elemento all'interno dell'elemento del relativo contenitore. Come un singolo elemento con i valori minimo e massimo della scala, i valori iniziale e finale dell'intervallo e il valore dell'indicatore di misura come attributi.|  
|Indicatore|Come elemento all'interno dell'elemento del relativo contenitore, in modo simile a un misuratore. Come un singolo elemento con il nome di stato attivo, gli stati disponibili e il valore dei dati come attributi.|  
  
 Per i report generati dall'estensione per il rendering XML sono inoltre previste le regole seguenti:  
  
-   Il rendering degli elementi e degli attributi XML viene eseguito rispettando l'ordine in cui sono visualizzati nella definizione del report.  
  
-   L'impaginazione viene ignorata.  
  
-   Il rendering di intestazioni e piè di pagina non viene eseguito.  
  
-   Il rendering degli elementi nascosti che non possono essere resi visibili tramite attivazione della visualizzazione non viene eseguito. Viene eseguito il rendering degli elementi inizialmente visibili e degli elementi nascosti che possono essere visibili mediante un elemento Toggle.  
  
-   **Immagini, linee ed elementi personalizzati del report** vengono ignorati.  
  
  
##  <a name="DataTypes"></a> Tipi di dati  
 All'attributo o all'elemento casella di testo viene assegnato un tipo di dati XSD in base ai valori visualizzati nella casella di testo.  
  
|Se tutti i valori della casella di testo sono|Viene assegnato il tipo di dati|  
|--------------------------------|---------------------------|  
|**Int16**, **Int32**, **Int64**, **UInt16**, **UInt32**, **UInt64**, **Byte**, **SByte**|**xsd:integer**|  
|**Decimal** (o **Decimal** e qualsiasi tipo di dati integer o byte)|**xsd:decimal**|  
|**Float** (o **Decimal** e qualsiasi tipo di dati integer o byte)|**xsd:float**|  
|**Double** (o **Decimal** e qualsiasi tipo di dati integer o byte)|**xsd:double**|  
|**DateTime o DateTime Offset**|**xsd:dateTime**|  
|**Time**|**xsd:string**|  
|**Boolean**|**xsd:boolean**|  
|**String**, **Char**|**xsd:string**|  
|Altri|**xsd:string**|  
  
  
##  <a name="XMLSpecificRenderingRules"></a> Regole di rendering specifiche di XML  
 Nelle sezioni seguenti viene descritta l'interpretazione degli elementi di un report da parte delle estensioni per il rendering XML.  
  
### <a name="report-body"></a>Corpo del report  
 Un report viene visualizzato come elemento radice del documento XML. Il nome dell'elemento deriva dalla proprietà DataElementName impostata nel riquadro Proprietà.  
  
 L'elemento del report include anche le definizioni di spazi dei nomi XML e gli attributi di riferimento allo schema. Le variabili sono indicate in grassetto:  
  
 <**Report** xmlns="**SchemaName**" xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>" xsi:**schemaLocation**="**SchemaNameReportURL**&amp;rc%3aSchema=true" Name="ReportName">  
  
 I valori delle variabili sono i seguenti:  
  
|Nome|valore|  
|----------|-----------|  
|Report|Report.DataElementName|  
|ReportURL|URL assoluto URLEncoded del report nel server.|  
|SchemaName|Report.SchemaName. Se Null, si utilizza Report.Name. Se si utilizza Report.Name, questo viene prima codificato con XmlConvert.EncodeLocalName.|  
|ReportName|Nome del report.|  
  
### <a name="text-boxes"></a>Caselle di testo  
 Le caselle di testo vengono visualizzate come elementi o attributi in base alla proprietà RDL DataElementStyle. Il nome dell'elemento o dell'attributo deriva dalla proprietà RDL TextBox.DataElementName.  
  
### <a name="charts-data-bars-and-sparklines"></a>Grafici, barre dei dati e grafici sparkline  
 Il rendering dei grafici, delle barre dei dati e dei grafici sparkline viene eseguito in XML. I dati sono strutturati.  
  
### <a name="gauges-and-indicators"></a>Misuratori e indicatori  
 Il rendering dei misuratori e degli indicatori viene eseguito in XML. I dati sono strutturati.  
  
### <a name="subreports"></a>Sottoreport  
 Un sottoreport viene visualizzato come elemento. Il nome dell'elemento deriva dalla proprietà RDL DataElementName. L'impostazione della proprietà TextBoxesAsElements del report sostituisce quella del sottoreport. Gli attributi XSLT e degli spazi dei nomi non vengono aggiunti all'elemento del sottoreport.  
  
### <a name="rectangles"></a>Rettangoli  
 Un rettangolo viene visualizzato come elemento. Il nome dell'elemento deriva dalla proprietà RDL DataElementName.  
  
### <a name="custom-report-items"></a>Elementi dei report personalizzati  
 Gli elementi di report personalizzati non sono visibili all'estensione per il rendering. Se nel report è presente un elemento personalizzato del report, l'estensione ne esegue il rendering come elemento del report convenzionale.  
  
### <a name="images"></a>Immagini  
 Il rendering delle immagini non viene eseguito.  
  
### <a name="lines"></a>Linee  
 Il rendering delle linee non viene eseguito.  
  
  
### <a name="tables-matrices-and-lists"></a>Tabelle, matrici ed elenchi  
 Tabelle, matrici ed elenchi vengono visualizzati come elemento. Il nome dell'elemento deriva dalla proprietà RDL DataElementName della Tablix.  
  
#### <a name="rows-and-columns"></a>Righe e colonne  
 Il rendering delle colonne viene eseguito all'interno delle righe.  
  
#### <a name="tablix-corner"></a>Angolo Tablix  
 Il rendering dell'angolo non viene eseguito. Viene eseguito il rendering solo del contenuto dell'angolo.  
  
#### <a name="tablix-cells"></a>Celle Tablix  
 Le celle Tablix vengono visualizzate come elementi. Il nome dell'elemento deriva dalla proprietà RDL DataElementName della cella.  
  
#### <a name="automatic-subtotals"></a>Subtotali automatici  
 Il rendering dei subtotali automatici Tablix non viene eseguito.  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>Elementi di colonne e righe che non si ripetono con un gruppo  
 Gli elementi che non si ripetono con un gruppo, ad esempio etichette, subtotali e totali, vengono visualizzati come elementi. Il nome dell'elemento deriva dalla proprietà RDL TablixMember.DataElementName.  
  
 La proprietà RDL TablixMember.DataElementOutput controlla se il rendering di un elemento non ripetuto viene eseguito o meno.  
  
 Se la proprietà DataElementName del membro Tablix non viene specificata, viene dinamicamente generato un nome per l'elemento non ripetuto nel formato seguente:  
  
 RowX   Per le righe non ripetute, dove X è un indice in base zero della riga all'interno dell'elemento padre corrente.  
  
 ColumnY   Per le colonne non ripetute, dove Y è un indice in base zero della colonna all'interno dell'elemento padre corrente.  
  
 Un'intestazione non ripetuta viene visualizzata come elemento figlio della riga o della colonna non ripetuta con un gruppo.  
  
 Il rendering di un membro non ripetuto senza celle Tablix corrispondenti non viene eseguito. Questa situazione può verificarsi nel caso di una cella Tablix che si estende in più di una colonna.  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>Righe e colonne che si ripetono con un gruppo  
 Il rendering di righe e colonne che si ripetono in un gruppo viene eseguito in base alle regole Tablix.DataElementOutput. Il nome dell'elemento deriva dalla proprietà DataElementName.  
  
 Ogni valore univoco all'interno di un gruppo viene visualizzato come elemento figlio del gruppo. Il nome dell'elemento deriva dalla proprietà Group.DataElementName.  
  
 Se il valore della proprietà DataElementOutput è uguale a Output, l'intestazione di un elemento ripetuto viene visualizzata come elemento figlio dell'elemento dettaglio.  
  
  
##  <a name="CustomFormatsXSLTransformations"></a> Formati personalizzati e trasformazioni XSL  
 I file XML generati dall'estensione per il rendering XML possono essere trasformati in quasi tutti i formati utilizzando trasformazioni XSL (XSLT). Questa funzionalità consente di produrre dati in formati non supportati dalle estensioni per il rendering esistenti. È consigliabile provare a utilizzare l'estensione per il rendering XML e le trasformazioni XSL prima di creare estensioni per il rendering personalizzate.  
  
  
##  <a name="DuplicateName"></a> Nomi duplicati  
 Se sono presenti nomi di elementi dati duplicati all'interno dello stesso ambito, verrà visualizzato un messaggio di errore del renderer.  
  
  
##  <a name="XSLTTransformations"></a> Trasformazioni XSLT  
 Il renderer XML può applicare una trasformazione XSLT lato server ai dati XML originali. Quando viene applicata una trasformazione XSLT, il renderer restituisce il contenuto trasformato anziché i dati XML originali. La trasformazione si verifica nel server, non nel client.  
  
 La trasformazione XSLT da applicare all'output viene definita nel file di definizione del report con la proprietà DataTransform del report o con il parametro XSLT *DeviceInfo* . Se viene impostato uno di questi valori, la trasformazione si verifica ogni volta che viene utilizzato il renderer XML. Quando si usano le sottoscrizioni, la trasformazione XSLT deve essere definita nella proprietà RDL DataTransform.  
  
 Se si specifica un file XSLT, tramite la proprietà di definizione DataTransform e l'impostazione delle informazioni sul dispositivo, la trasformazione XSLT specificata in DataTransform si verifica per prima, seguita dalla trasformazione XSLT specificata tramite le impostazioni delle informazioni sul dispositivo.  
  
  
###  <a name="DeviceInfo"></a> Impostazioni relative alle informazioni sul dispositivo  
 È possibile modificare alcune impostazioni predefinite per questo renderer modificando le impostazioni relative alle informazioni sul dispositivo, incluse le seguenti:  
  
-   Trasformazione (XSLT) da applicare al codice XML  
  
-   Tipo MIME del documento XML  
  
-   Applicazione o meno di stringhe di formato ai dati  
  
-   Rientro o meno dell'output XML  
  
-   Inclusione o meno del nome XML Schema  
  
-   Codifica del documento XML  
  
-   Estensione del file del documento XML.  
  
 Per altre informazioni, vedere [Impostazioni relative alle informazioni sul dispositivo XML](../../reporting-services/xml-device-information-settings.md).  
  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
