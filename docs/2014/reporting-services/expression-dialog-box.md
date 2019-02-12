---
title: Finestra di dialogo espressione | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
- sql12.rtp.rptdesigner.expression.f1
helpviewer_keywords:
- Expression dialog box [Reporting Services]
ms.assetid: e6c74ccb-4594-4d4f-b958-618d710e34eb
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 43f27ea78bec3f7b81f49d44a6bd56274367f2b5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021686"
---
# <a name="expression-dialog-box"></a>Finestra di dialogo Espressione
  Usare la **espressione** finestra di dialogo per scrivere [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] le proprietà degli elementi delle espressioni di report. Le espressioni possono essere utilizzate per impostare molte proprietà, ad esempio il colore, il tipo di carattere e i bordi. In fase di esecuzione, il componente Elaborazione report valuta le espressioni e sostituisce il valore della proprietà con il risultato.  
  
 Un'espressione può essere semplice o complessa. È possibile digitare le espressioni semplici direttamente in una casella di testo nell'area di progettazione o in una finestra di dialogo. Per creare espressioni complesse, usare il **espressione** nella finestra di dialogo. È possibile creare un'espressione alla volta. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md).  
  
 Per aprire la finestra di dialogo **Espressione** , fare clic sul pulsante Espressione (**fx**) disponibile nelle finestre di dialogo oppure scegliere **Espressione** dal menu di scelta rapida o selezionarlo negli elenchi a discesa nel riquadro Proprietà. Per altre informazioni, vedere [uso delle espressioni nei report di &#40;Generatore Report e SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md).  
  
 La finestra di dialogo **Espressione** include una finestra del codice, un albero delle categorie, gli elementi delle categorie, un riquadro di descrizione e un riquadro di esempio.  
  
 Poiché la finestra di dialogo **Espressione** è sensibile al contesto, le descrizioni e gli elementi delle categorie variano a seconda della categoria di espressione che si sta usando. Questa finestra di dialogo supporta IntelliSense, il completamento delle istruzioni, esempi di chiamate a funzioni e la colorazione della sintassi, che consente di rilevare facilmente gli errori.  
  
## <a name="expression-constructs"></a>Costrutti di espressione  
 Le espressioni iniziano con un segno di uguale (=) e possono includere costanti, valori letterali, operatori e riferimenti a campi predefiniti, raccolte predefinite, funzioni predefinite, funzioni della libreria run-time di [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], classi Common Language Runtime di [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e funzioni personalizzate. Nell'elenco seguente vengono descritti le categorie e i valori che è possibile aggiungere in un'espressione.  
  
 **Imposta espressione per:**  _\<PropertyName >_  
 Nome della proprietà per cui si definisce un'espressione. È anche possibile impostare questa proprietà, per nome, nel riquadro Proprietà.  
  
 **Costanti**  
 Consente di visualizzare un elenco di valori predefiniti validi per la proprietà corrente, nel caso di proprietà basate su costanti. Ad esempio, una proprietà basata su colore indica nomi di colore validi. Per una proprietà con un tipo di dati booleano, i valori sono `True` e `False`.  
  
 Non tutti gli elementi che supportano le espressioni possono essere impostati su una costante. Se una proprietà non può essere impostata su un valore costante, nel riquadro di descrizione verrà indicata questa informazione.  
  
 **Campi predefiniti**  
 Consente di visualizzare un elenco degli elementi della raccolta globale che possono essere utilizzati in un'espressione. Alcune raccolte sono supportate solo dopo la pubblicazione del report nel server. Per altre informazioni, vedere [Riferimenti alle raccolte predefinite Globals e Users &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
 **Parametri**  
 Consente di visualizzare un elenco di parametri del report.  
  
 **Campi (**  _\<set di dati selezionato >_ **)**  
 Consente di visualizzare l'elenco di campi per il set di dati selezionato nella categoria Set di dati. Fare doppio clic su un campo per copiarlo nella casella **Espressione** .  
  
 **Set di dati**  
 Consente di visualizzare un elenco di set di dati disponibili e i relativi campi membri.  
  
 **Variabili**  
 Consente di visualizzare un elenco di variabili del report. Per altre informazioni, vedere [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md).  
  
 **Operatori**  
 Consente di visualizzare gli operatori che è possibile includere nella modifica di un calcolo o di una stringa. Per altre informazioni, vedere [Operatori nelle espressioni &#40;Generatore report e SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md).  
  
 **Funzioni comuni**  
 Consente di visualizzare funzioni comuni, raggruppate per tipo. Quando si seleziona una funzione nel riquadro Elemento, verranno visualizzati una descrizione e un esempio.  
  
 Le funzioni comuni includono le funzioni predefinite di report e aggregazione, le funzioni della libreria run-time di [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e le classi Common Language Runtime (CLR) di [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] negli spazi dei nomi <xref:System.Math> e <xref:System.Convert>. È anche possibile aggiungere riferimenti a classi CLR e assembly esterni non riportati nell'elenco di categorie. Per altre informazioni, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 Finestra del codice  
 Utilizzare la finestra del codice nel riquadro superiore per digitare un'espressione. All'apertura della finestra di dialogo **Espressione** , la finestra del codice contiene l'espressione. che può essere sostituita o modificata. È possibile aggiungere chiamate a funzioni, operatori, costanti, campi, parametri, elementi delle raccolte globali e riferimenti a codice personalizzato. Le modifiche apportate vengono visualizzate nella finestra del codice.  
  
 Una sottolineatura rossa ondulata indica un errore di sintassi. Soffermare il puntatore sul testo sottolineato per visualizzare il messaggio di errore.  
  
 Quando si digitano i termini della raccolta globale seguiti da un separatore di punteggiatura, verrà visualizzato un elenco a discesa di membri o proprietà disponibili. Da questo elenco a discesa è possibile digitare i primi caratteri, seguiti da un carattere di tabulazione, per consentire il riempimento automatico della selezione.  
  
 Quando si digita il nome di una funzione seguito da una parentesi aperta, verrà visualizzata una descrizione comando con informazioni sui parametri e sui valori restituiti della funzione.  
  
 **Categoria**  
 Consente di visualizzare categorie di espressioni. La scelta di una categoria stabilisce un contesto per la creazione di un'espressione e comporta la modifica dell'elenco di valori validi nel riquadro Elemento. Ad esempio, per un'espressione per il valore di una casella di testo, espandere funzioni comuni e selezionare le funzioni di aggregazione da visualizzare `Avg`, `Count`e altre funzioni il **elemento** riquadro.  
  
 **Elemento**  
 Consente di visualizzare l'elenco di valori validi per la categoria selezionata. Fare doppio clic su un elemento per aggiungere il testo dell'espressione per l'elemento specifico in corrispondenza del punto di inserimento nella finestra del codice.  
  
 **Valori**  
 A seconda della categoria e dell'elemento selezionato, il terzo riquadro contiene una descrizione, un'espressione di esempio o un elenco di valori validi. Trascinare il bordo della finestra di dialogo per ampliare l'area di esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)   
 [Aggiungere un'espressione &#40;Generatore report e SSRS&#41;](report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
