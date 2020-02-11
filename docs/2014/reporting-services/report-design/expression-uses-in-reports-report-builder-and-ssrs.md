---
title: Uso delle espressioni nei report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 13fd93468fafb99a5bd2869c207496b21dcb8174
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105900"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>Utilizzo delle espressioni nei report (Generatore report e SSRS)
  Le espressioni sono usate nella definizione del report per specificare o calcolare valori per parametri, query, filtri, proprietà degli elementi del report, definizioni di gruppo e di ordinamento, proprietà delle caselle di testo, segnalibri, mappe documento, contenuto dinamico dell'intestazione e del piè di pagina, immagini e definizioni delle origini dati dinamiche. In questo argomento vengono forniti esempi delle numerose posizioni in cui è possibile utilizzare le espressioni per modificare il contenuto o l'aspetto di un report. Non si tratta tuttavia di un elenco completo. È possibile impostare un'espressione per qualsiasi proprietà in una finestra di dialogo che contiene il pulsante di espressione (**fx**) o in un elenco a discesa in cui è visualizzato **\<Espressione...>**.  
  
 Le espressioni possono essere semplici o complesse. Le *espressioni semplici* contengono un riferimento a un singolo campo del set di dati, un parametro o un campo predefinito. Le espressioni complesse possono contenere più riferimenti incorporati, operatori e chiamate di funzione. Ad esempio, un'espressione complessa potrebbe includere la funzione Sum applicata al campo Sales.  
  
 Le espressioni sono scritte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]in. Un'espressione inizia con un segno di uguale (=) seguito da una combinazione di riferimenti a raccolte predefinite, quali parametri e campi di set di dati, costanti, funzioni e operatori.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a>Utilizzo di espressioni semplici  
 e vengono visualizzate tra parentesi nell'area di progettazione e nelle finestre di dialogo. Un campo del set di dati viene ad esempio visualizzato come `[ProductID]`. Le espressioni semplici vengono create automaticamente quando si trascina un campo da un set di dati in una casella di testo. Viene creato un segnaposto e l'espressione definisce il valore sottostante. È inoltre possibile digitare le espressioni direttamente in una cella o in una casella di testo dell'area dati, sia nell'area di progettazione che in una finestra di dialogo, ad esempio `[ProductID]`.  
  
 Nella tabella seguente sono elencati esempi delle modalità di utilizzo delle espressioni semplici. Viene fornita la descrizione della funzionalità, della proprietà da impostare, della finestra di dialogo in genere utilizzata per l'impostazione e del valore per la proprietà. È possibile digitare l'espressione semplice direttamente nell'area di progettazione, in una finestra di dialogo o nel riquadro Proprietà oppure modificarla nella finestra di dialogo Espressione, procedendo come per qualsiasi espressione.  
  
|Funzionalità|Proprietà, contesto e finestra di dialogo|Valore proprietà|  
|-------------------|---------------------------------------|--------------------|  
|Specificare un campo del set di dati da visualizzare in una casella di testo.|Proprietà Value per un segnaposto in una casella di testo. Usare la finestra di dialogo **Proprietà segnaposto, Generale**.|`[Sales]`|  
|Aggregare valori per un gruppo.|Proprietà Value per un segnaposto in una riga associata a un gruppo Tablix. Usare la finestra di dialogo **Proprietà casella di testo**.|`[Sum(Sales)]`|  
|Includere un numero di pagina.|Proprietà Value per un segnaposto in una casella di testo posizionata in un'intestazione di pagina. Usare la finestra di dialogo **Proprietà casella di testo, Generale**.|`[&PageNumber]`|  
|Visualizzare un valore di parametro selezionato.|Proprietà Value per un segnaposto in una casella di testo nell'area di progettazione. Usare la finestra di dialogo **Proprietà casella di testo, Generale**.|`[@SalesThreshold]`|  
|Specificare una definizione di gruppo per un'area dati.|Espressione di raggruppamento nel gruppo Tablix. Usare la finestra di dialogo **Proprietà gruppo Tablix, Generale**.|`[Category]`|  
|Escludere un valore di campo specifico da una tabella.|Equazione di filtro nella Tablix. Usare la finestra di dialogo **Proprietà Tablix, Filtri**.|Come tipo di dati selezionare **Integer**.<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|Includere solo un valore specifico per un filtro di gruppo.|Equazione di filtro nel gruppo Tablix. Usare la finestra di dialogo **Proprietà gruppo Tablix, Filtri**.|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|Escludere valori specifici per più campi da un set di dati.|Equazione di filtro per un gruppo in una Tablix. Usare la finestra di dialogo **Proprietà Tablix, Filtri**.|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|Specificare l'ordinamento in base a un campo esistente in una tabella.|Espressione di ordinamento nella Tablix. Usare la finestra di dialogo **Proprietà Tablix, Ordinamento**.|`[SizeSortOrder]`|  
|Collegare un parametro di query a un parametro di report.|Raccolta di parametri nel set di dati. Usare la finestra di dialogo **Proprietà set di dati, Parametri**.|`[@Category]`<br /><br /> `[@Category]`|  
|Passare un parametro da un report principale a un sottoreport.|Raccolta di parametri nel sottoreport. Usare la finestra di dialogo **Proprietà sottoreport, Parametri**.|`[@Category]`<br /><br /> `[@Category]`|  
  
 
  
##  <a name="Complex"></a>Utilizzo di espressioni complesse  
 Le espressioni complesse possono contenere più riferimenti, operatori e chiamate di funzione predefiniti e vengono visualizzate nell'area di progettazione come `<<Expr>>`. Per visualizzare o modificare il testo dell'espressione, è necessario aprire la finestra di dialogo **Espressione** o digitare direttamente nel riquadro Proprietà. Nella tabella seguente sono elencate le modalità di utilizzo standard di un'espressione complessa per visualizzare o organizzare i dati oppure modificare l'aspetto del report. Vengono ad esempio fornite indicazioni sulla proprietà da impostare, sulla finestra di dialogo in genere usata per l'impostazione e sul valore per la proprietà. È possibile digitare un'espressione direttamente in una finestra di dialogo, nell'area di progettazione o nel riquadro Proprietà.  
  
|Funzionalità|Proprietà, contesto e finestra di dialogo|Valore proprietà|  
|-------------------|---------------------------------------|--------------------|  
|Calcolare i valori di aggregazione per un set di dati.|Proprietà Value per un segnaposto in una casella di testo. Usare la finestra di dialogo **Proprietà segnaposto, Generale**.|`=First(Fields!Sales.Value,"DataSet1")`|  
|Concatenare testo ed espressioni nella stessa casella di testo.|Value per un segnaposto in una casella di testo posizionata in un'intestazione o in un piè di pagina. Usare la finestra di dialogo **Proprietà segnaposto, Generale**.|`="This report began processing at " & Globals!ExecutionTime`|  
|Calcolare un valore di aggregazione per un set di dati in un ambito diverso.|Value per un segnaposto in una casella di testo posizionata in un gruppo Tablix. Usare la finestra di dialogo **Proprietà segnaposto, Generale**.|`=Max(Fields!Total.Value,"DataSet2)`|  
|Formattare i dati in una casella di testo in base al valore.|Colore per un segnaposto in una casella di testo nella riga dei dettagli di una Tablix. Usare la finestra di dialogo **Proprietà casella di testo, Carattere**.|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|Calcolare un valore una volta per farvi riferimento in tutto il report.|Value per una variabile del report. Usare la finestra di dialogo **Proprietà report, Variabili**.|`=Variables!MyCalculation.Value`|  
|Includere valori specifici per più campi di un set di dati.|Equazione di filtro per un gruppo in una Tablix. Usare la finestra di dialogo **Proprietà Tablix, Filtri**.|Come tipo di dati selezionare **Boolean**.<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|Nascondere una casella di testo nell'area di progettazione, la cui visibilità può essere attivata o disattivata dall'utente mediante un parametro booleano denominato *Show*.|Hiddenproperty in una casella di testo. Usare la finestra di dialogo **Proprietà casella di testo, Visibilità**.|`=Not Parameters!`*Mostra\<>parametro booleano*`.Value`|  
|Specificare il contenuto dinamico dell'intestazione o del piè di pagina.|Value per un segnaposto in una casella di testo posizionata nell'intestazione o nel piè di pagina.|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|Specificare un'origine dati in modo dinamico utilizzando un parametro.|Stringa di connessione nell'origine dati. Usare la finestra di dialogo **Proprietà origine dati, Generale**.|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|Identificare tutti i valori per un parametro multivalore scelto dall'utente.|Value per un segnaposto in una casella di testo. Usare la finestra di dialogo **Proprietà Tablix, Filtri**.|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|Specificare interruzioni di pagina ogni 20 righe in una Tablix senza altri gruppi.|Espressione di raggruppamento per un gruppo in una Tablix. Usare la finestra di dialogo **Proprietà gruppo Tablix, Interruzioni di pagina**. Selezionare l'opzione **Tra ogni istanza di un gruppo**.|`=Ceiling(RowNumber(Nothing)/20)`|  
|Specificare la visibilità condizionale in base a un parametro.|Proprietà Hidden per una Tablix. Usare la finestra di dialogo **Proprietà Tablix, Visibilità**.|`=Not Parameters!<`*parametro booleano*`>.Value`|  
|Specificare una data formattata per determinate impostazioni cultura.|Value per un segnaposto di una casella di testo in un'area dati. Usare la finestra di dialogo **Proprietà casella di testo, Generale**.|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|Concatenare una stringa e un numero nel formato di percentuale a due cifre decimali.|Value per un segnaposto di una casella di testo in un'area dati. Usare la finestra di dialogo **Proprietà casella di testo, Generale**.|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Nascondi un elemento &#40;Generatore report e SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
