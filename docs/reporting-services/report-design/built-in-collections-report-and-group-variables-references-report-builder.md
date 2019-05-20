---
title: Riferimenti a raccolte di variabili di report e di gruppo (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 97123f3e9802ddbdf452f66e83a1b3c00f99764d
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581776"
---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>Raccolte predefinite - Riferimenti a variabili di report e di gruppo (Generatore report)
  Quando un calcolo complesso viene utilizzato più volte nelle espressioni di un report, è possibile creare una variabile che può essere di report o di gruppo. I nomi delle variabili devono essere univoci in un report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>Variabili di report  
 Utilizzare una variabile di report per memorizzare un valore per i calcoli dipendenti dal tempo, ad esempio tassi valutari o timestamp, oppure per un calcolo complesso a cui si fa riferimento più volte. Per impostazione predefinita, una variabile di report viene calcolata una sola volta e può essere utilizzata nelle espressioni di un intero report. Inoltre, le variabili di report sono di sola lettura. È possibile modificare l'impostazione predefinita in modo da abilitare la modalità di lettura/scrittura per una variabile di report. Il valore in una variabile di report viene mantenuto per tutta una sessione, fino alla nuova elaborazione del report.  
  
 Per aggiungere una variabile di report, aprire la finestra di dialogo **Proprietà report** , fare clic su **Variabili**e quindi specificare un nome e un valore. I nomi sono stringhe con distinzione tra maiuscole e minuscole che iniziano con una lettera e non contengono spazi. Un nome può contenere lettere, numeri o caratteri di sottolineatura (_).  
  
 Per fare riferimento alla variabile in un'espressione, utilizzare la sintassi di raccolta globale, ad esempio `=Variables!CustomTimeStamp.Value`. Nell'area di progettazione il valore viene visualizzato in una casella di testo come `<<Expr>>`.  
  
 È possibile utilizzare le variabili del report come indicato di seguito:  
  
-   **Uso in sola lettura** Impostare un valore una sola volta in modo da creare una costante per la sessione del report, ad esempio un timestamp.  
  
     Dato che le espressioni nelle caselle di testo vengono valutate su richiesta quando un utente scorre un report, i valori dinamici, ad esempio un'espressione che include la funzione `Now()` che restituisce l'ora del giorno, possono restituire valori diversi se si passa a una pagina successiva e a una precedente tramite il pulsante **Indietro** . Impostando il valore di una variabile di report sull'espressione `=Now()`e aggiungendo quindi tale variabile all'espressione, si garantisce l'utilizzo dello stesso valore per tutta l'elaborazione del report.  
  
-   **Uso in lettura/scrittura** Impostare un valore una sola volta e serializzarlo all'interno di una sessione di report. L'opzione di lettura/scrittura per le variabili rappresenta un'alternativa migliore rispetto all'utilizzo di una variabile statica nel blocco di codice nella definizione del report.  
  
     Quando si deseleziona l'opzione **Sola lettura** per una variabile, la proprietà Writable per la variabile viene impostata su **true**. Per aggiornare il valore generato da un'espressione, usare il metodo SetValue, ad esempio `=Variables!MyVariable.SetValue("123")`.  
  
    > [!NOTE]  
    >  Non è possibile controllare quando l'elaboratore di report inizializza una variabile o valuta un'espressione che aggiorna una variabile. L'ordine di esecuzione per l'inizializzazione delle variabili non è definito.  
  
 Per altre informazioni, vedere [Anteprima di report in Generatore report](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="group-variables"></a>Variabili di gruppo  
 Utilizzare una variabile di gruppo per calcolare un'espressione complessa nell'ambito di un gruppo. Una variabile di gruppo è valida solo nell'ambito del gruppo e dei relativi gruppi figlio.  
  
 Si supponga, ad esempio, che in un'area dati vengano visualizzati dati di inventario per elementi che rientrano in diverse categorie di imposta e che si desideri applicare aliquote d'imposta diverse per ogni categoria. I dati verranno raggruppati in base alla categoria e verrà definita una variabile *Tax* nel gruppo padre. Verrà quindi definita una variabile di gruppo per *ItemTax* per ogni categoria di imposta e ogni sottogruppo di categorie diverso verrà assegnato alla variabile di gruppo corretta. Esempio:  
  
-   Per il gruppo padre basato su `[Category]`, definire la variabile *Tax* con un valore `[Tax]`. Si supponga che i valori di categoria siano Food e Clothing.  
  
-   Per il gruppo figlio basato su `[Subcategory]`, definire la variabile *ItemsTax* come `=Variables!Tax.Value * Sum(Fields!Price.Value)`. Si supponga che i valori di sottocategoria per la categoria Food siano Beverages e Bread e che i valori di sottocategoria per Clothing siano Shirts e Hats.  
  
-   Per una casella di testo in una riga del gruppo figlio, aggiungere l'espressione `=Variables!ItemsTax.Value`.  
  
     Nella casella di testo viene visualizzata l'imposta totale per Beverages e Bread utilizzando l'imposta di Food e per Shirts e Hats utilizzando l'imposta di Clothing.  
  
 Per aggiungere una variabile di gruppo, aprire la finestra di dialogo **Proprietà gruppo Tablix** , fare clic su **Variabili**e quindi specificare un nome e un valore. La variabile di gruppo viene calcolata una volta per ogni valore di gruppo univoco.  
  
 Per fare riferimento alla variabile in un'espressione, utilizzare la sintassi di raccolta globale, ad esempio `=Variables!GroupDescription.Value`. Nell'area di progettazione il valore viene visualizzato in una casella di testo come `<<Expr>>`.  
  
## <a name="see-also"></a>Vedere anche  
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
