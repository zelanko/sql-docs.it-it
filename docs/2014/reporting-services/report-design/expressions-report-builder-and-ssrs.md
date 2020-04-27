---
title: Espressioni (Generatore report e SSRS) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 76d3ac86-650c-46fe-8086-8b3edcea3882
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 3660ecee1271d4fd2673b0dfe9107a8fb5c52e88
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67413011"
---
# <a name="expressions-report-builder-and-ssrs"></a>Espressioni (Generatore report e SSRS)

Le espressioni vengono ampiamente utilizzate in un report per recuperare, calcolare, visualizzare, raggruppare, ordinare, filtrare, parametrizzare e formattare i dati. Molte proprietà dell'elemento del report possono essere impostate su un'espressione tramite la quale è possibile controllare il contenuto, la progettazione e l'interattività del report. Le espressioni sono scritte in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], salvate nella definizione del report e valutate dall'elaboratore di report durante l'esecuzione del report.  

A differenza di applicazioni come [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office Excel, in cui è possibile usare i dati direttamente in un foglio di lavoro, in un report è possibile gestire espressioni che sono segnaposto per i dati. Per visualizzare i dati effettivi dalle espressioni valutate, è necessario visualizzare in anteprima il report. Durante l'esecuzione del report, tramite l'elaboratore di report è possibile valutare ogni espressione poiché vengono combinati i dati del report con gli elementi di layout del report quali tabelle e grafici.  

Quando si progetta un report, molte espressioni degli elementi del report vengono impostate automaticamente. Ad esempio, quando si trascina un campo dal riquadro dei dati in una cella della tabella nell'area di progettazione del report, il valore della casella di testo viene impostato su un'espressione semplice per il campo. Nel riquadro dei dati riportato nella figura seguente vengono visualizzate le opzioni ID Name, SalesTerritory, Code e Sales dei campi del set di dati. Alla tabella sono stati aggiunti tre campi: [Name], [Code] e [Sales]. La notazione [Name] nell'area di progettazione rappresenta l'espressione `=Fields!Name.Value`sottostante.  

![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  

Quando si visualizza in anteprima il report, tramite l'elaboratore di report l'area dati della tabella viene combinata con i dati effettivi della connessione dati e viene visualizzata una riga nella tabella per ogni riga nel set di risultati.  

Per immettere espressioni manualmente, selezionare un elemento nell'area di progettazione e utilizzare menu di scelta rapida e finestre di dialogo per impostare le proprietà dell'elemento. Quando viene visualizzato il pulsante ***(fx)*** o il valore `<Expression>` in un elenco a discesa, è possibile impostare la proprietà su un'espressione. Per altre informazioni, vedere [Aggiungere un'espressione &#40;Generatore report e SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)sottostante.  

Per ulteriori informazioni ed esempi, vedere gli argomenti seguenti:  

-   [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  

-   [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  

-   [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  

-   [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](group-expression-examples-report-builder-and-ssrs.md)  

-   [Esercitazioni &#40;Generatore report&#41;](../report-builder-tutorials.md)  

-   [Esercitazioni su Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  

-   [Esempi di report (Generatore report e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  

Per sviluppare espressioni complesse o espressioni che consentono l'utilizzo di codice o assembly personalizzati, si consiglia di usare Progettazione report di [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)sottostante.  

> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  

##  <a name="understanding-simple-and-complex-expressions"></a><a name="Types"></a>Informazioni sulle espressioni semplici e complesse  
Le espressioni iniziano con un segno di uguale (=) e sono [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]scritte in. Nelle espressioni può essere inclusa una combinazione di costanti, operatori e riferimenti a valori predefiniti, ad esempio campi, raccolte e funzioni, e a codice esterno o personalizzato.  

Le espressioni possono essere utilizzate per specificare il valore di numerose proprietà dell'elemento del report. Le proprietà più comuni sono valori per caselle di testo e testo segnaposto. In genere, se in una casella di testo è contenuta un'unica espressione, tale espressione è il valore della proprietà della casella di testo. Se in una casella di testo sono contenute più espressioni, ognuna di queste rappresenta il valore di testo segnaposto nella casella di testo.  

Per impostazione predefinita, le espressioni vengono visualizzate nell'area di progettazione del report come espressioni *semplici* o *complesse*.  

-   **Semplice** Espressione contenente un riferimento a un singolo elemento in una raccolta predefinita, ad esempio un campo del set di dati, un parametro oppure un campo predefinito. Un'espressione semplice viene visualizzata tra parentesi nell'area di progettazione. `[FieldName]` , ad esempio, corrisponde all'espressione sottostante `=Fields!FieldName.Value`. Le espressioni semplici vengono create automaticamente quando si crea il layout del report e si trascinano gli elementi dal riquadro dei dati del report nell'area di progettazione. Per altre informazioni sui simboli che rappresentano raccolte predefinite diverse, vedere [Informazioni sui simboli di prefissi in espressioni semplici](#DisplayText).  

-   **Complessa** Espressione contenente riferimenti a più riferimenti, operatori e chiamate di funzioni predefiniti. Un'espressione complessa viene visualizzata come <\<Expr>> se il valore dell'espressione include più riferimenti semplici. Per visualizzare l'espressione, posizionare il puntatore del mouse su tale espressione e utilizzare la descrizione comando. Per modificare l'espressione, aprirla nella finestra di dialogo **Espressione** .  

Nella figura seguente vengono mostrate espressioni semplici e complesse tipiche sia per le caselle di testo sia per il testo segnaposto.  

![rs_ExpressionDefaultFormat](../media/rs-expressiondefaultformat.gif "rs_ExpressionDefaultFormat")  

Per visualizzare valori di esempio anziché il testo per le espressioni, applicare la formattazione alla casella di testo o al testo segnaposto. Nella figura seguente viene mostrata l'area di progettazione del report attivata o disattivata per la visualizzazione dei valori di esempio:  

![rs_ExpressionSampleValuesFormat](../media/rs-expressionsamplevaluesformat.gif "rs_ExpressionSampleValuesFormat")  

Per altre informazioni, vedere [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md).  

## <a name="understanding-prefix-symbols-in-simple-expressions"></a><a name="DisplayText"></a> Informazioni sui simboli di prefissi in espressioni semplici  

Nelle espressioni semplici vengono utilizzati simboli per indicare se il riferimento è a un campo, un parametro, una raccolta predefinita o la raccolta ReportItems. Nella tabella seguente vengono riportati esempi di testo visualizzato e di quello relativo alle espressioni:  

|Item|Esempio di testo visualizzato|Esempio di testo dell'espressione|  
|----------|--------------------------|-----------------------------|  
|Campi del set di dati|`[Sales]`<br /><br /> `[SUM(Sales)]`<br /><br /> `[FIRST(Store)]`|`=Fields!Sales.Value`<br /><br /> `=Sum(Fields!Sales.Value)`<br /><br /> `=First(Fields!Store.Value)`|  
|Parametri di report|`[@Param]`<br /><br /> `[@Param.Label]`|`=Parameters!Param.Value`<br /><br /> `=Parameters!Param.Label`|  
|Campi predefiniti|`[&ReportName]`|`=Globals!ReportName.Value`|  
|Caratteri letterali utilizzati per il testo visualizzato|`\[Sales\]`|`[Sales]`|  



##  <a name="writing-complex-expressions"></a><a name="References"></a>Scrittura di espressioni complesse  
Nelle espressioni possono essere inclusi riferimenti a funzioni, operatori, costanti, campi, parametri, elementi di raccolte predefinite nonché a codice personalizzato o assembly personalizzati incorporati.  

> [!NOTE]
>  Per sviluppare espressioni complesse o espressioni che consentono l'utilizzo di codice o assembly personalizzati, si consiglia di usare Progettazione report di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)sottostante.  

Nella tabella seguente vengono elencati i tipi di riferimenti che è possibile includere in un'espressione:  

|Riferimenti|Descrizione|Esempio|  
|----------------|-----------------|-------------|  
|[Costanti](expressions-report-builder-and-ssrs.md)|Vengono descritte le costanti a cui è possibile accedere in modo interattivo per le proprietà che richiedono valori costanti, ad esempio i colori dei caratteri.|`="Blue"`|  
|[Operatori](operators-in-expressions-report-builder-and-ssrs.md)|Vengono descritti gli operatori che possono essere utilizzati per la combinazione di riferimenti in un'espressione. L'operatore `&`, ad esempio, viene utilizzato per la concatenazione di stringhe.|`="The report ran at: " & Globals!ExecutionTime & "."`|  
|[Raccolte predefinite](built-in-collections-in-expressions-report-builder.md)|Vengono descritte le raccolte predefinite che è possibile includere in un'espressione, ad esempio, `Fields`, `Parameters`e `Variables`.|`=Fields!Sales.Value`<br /><br /> `=Parameters!Store.Value`<br /><br /> `=Variables!MyCalculation.Value`|  
|[Funzioni predefinite di report e di aggregazione](report-builder-functions-aggregate-functions-reference.md)|Vengono descritte le funzioni predefinite, ad esempio `Sum` o `Previous`, cui è possibile accedere da un'espressione.|`=Previous(Sum(Fields!Sales.Value))`|  
|[Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)|Viene descritto come accedere alle classi CLR predefinite <xref:System.Math> e <xref:System.Convert>, ad altre classi CLR, a funzioni della libreria di runtime di [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o a metodi da un assembly esterno.<br /><br /> Viene descritto come accedere a codice personalizzato incorporato nel report o compilato e installato come assembly personalizzato sia nel client che nel server di report.|`=Sum(Fields!Sales.Value)`<br /><br /> `=CDate(Fields!SalesDate.Value)`<br /><br /> `=DateAdd("d",3,Fields!BirthDate.Value)`<br /><br /> `=Code.ToUSD(Fields!StandardCost.Value)`|  



##  <a name="validating-expressions"></a><a name="Valid"></a>Convalida di espressioni  
Quando si crea un'espressione per una proprietà specifica dell'elemento del report, i riferimenti che è possibile includere in un'espressione dipendono dai valori accettati dalla proprietà dell'elemento del report e dall'ambito nel quale viene valutata la proprietà. Ad esempio:  

-   Per impostazione predefinita, l'espressione [Sum] consente di calcolare la somma di dati presenti nell'ambito al momento della valutazione dell'espressione. Per una cella della tabella, l'ambito dipende dalle appartenenze ai gruppi di righe e di colonne. Per altre informazioni, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)sottostante.  

-   Per il valore di una proprietà Font, tramite il valore deve essere restituito il nome di un tipo di carattere.  

-   La sintassi dell'espressione viene convalidata in fase di progettazione mentre la convalida dell'ambito dell'espressione viene eseguita durante la pubblicazione del report. Per convalide che dipendono dai dati effettivi, gli errori possono essere rilevati solo in fase di esecuzione. Alcune di queste espressioni generano un messaggio di errore di tipo #Errore nel report sottoposto a rendering. Per determinare i problemi relativi a questo tipo di errore, è necessario utilizzare Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. In Progettazione report è disponibile una finestra Output nella quale vengono fornite ulteriori informazioni su questi errori.  

Per altre informazioni, vedere [Riferimento dell'espressione &#40;Generatore report e SSRS&#41;](expression-reference-report-builder-and-ssrs.md)sottostante.  

## <a name="in-this-section"></a><a name="Section"></a>Contenuto della sezione

[Aggiungere un'espressione &#40;Generatore report e SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)  

[Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  

[Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  

[Riferimento dell'espressione &#40;Generatore report e SSRS&#41;](expression-reference-report-builder-and-ssrs.md)  

## <a name="see-also"></a>Vedi anche

- [Finestra di dialogo Espressione](../expression-dialog-box.md)   
- [Finestra di dialogo dell'espressione &#40;Generatore report&#41;](../expression-dialog-box-report-builder.md)