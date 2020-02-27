---
title: Creare un gruppo di gerarchie ricorsive (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2d1a73f72cc267b8a58c70dd4ea958be3560a4fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080555"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>Creare un gruppo di gerarchie ricorsive (Generatore report e SSRS)
Nei report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , un gruppo di gerarchie ricorsive organizza i dati da un unico set di dati di un report in cui sono inclusi più livelli gerarchici, ad esempio il report per definire la struttura di relazioni tra dipendenti e manager in una gerarchia organizzativa.  
  
 Prima che sia possibile organizzare i dati in una tabella come un gruppo di gerarchie ricorsive, è necessario disporre di un unico set di dati che contiene tutti i dati gerarchici. È necessario disporre di campi separati per gli elementi da raggruppare e per l'elemento in base al quale eseguire il raggruppamento. Un set di dati, ad esempio, in cui si desidera raggruppare i dipendenti in modo ricorsivo sotto il loro superiore, potrebbe contenere un nome, un nome di dipendente, un ID dipendente e un ID responsabile.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-recursive-hierarchy-group"></a>Per creare un gruppo di gerarchie ricorsive  
  
1.  Nella visualizzazione della struttura aggiungere una tabella e trascinare i campi del set di dati da visualizzare. In genere, il campo che si desidera mostrare come una gerarchia si trova nella prima colonna.  
  
2.  Fare clic con il pulsante destro del mouse in un punto qualsiasi della tabella per selezionarla. Nel riquadro di raggruppamento viene visualizzato il gruppo di dettagli per la tabella selezionata. Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse su **Dettagli**, quindi scegliere **Modifica gruppo**. Verrà visualizzata la finestra di dialogo **Proprietà gruppo** .  
  
3.  In **Espressioni di raggruppamento**fare clic su **Aggiungi**. Nella griglia verrà visualizzata una nuova riga.  
  
4.  Nell'elenco **Raggruppa in base a** digitare o selezionare il campo da raggruppare.  
  
5.  Fare clic su **Avanzate**.  
  
6.  Nell'elenco **Elemento padre ricorsivo** immettere o selezionare il campo in base al quale eseguire il raggruppamento.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Eseguire il report. Nel report viene visualizzato il gruppo di gerarchie ricorsive, anche se non è presente alcun rientro per indicare la gerarchia.  
  
## <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>Per formattare un gruppo di gerarchie ricorsive con livelli di rientro  
  
1.  Fare clic sulla casella di testo che contiene il campo cui si desidera aggiungere livelli di rientro per visualizzare un formato di gerarchia. Le proprietà per la casella di testo verranno visualizzate nel riquadro Proprietà.  
  
    > [!NOTE]  
    >  Se il riquadro Proprietà non è visualizzato, fare clic su **Proprietà** nella scheda **Visualizza** .  
  
2.  Nel riquadro Proprietà espandere il nodo **Riempimento**, fare clic su **A sinistra**, quindi selezionare **\<Espressione...>** dall'elenco a discesa.  
  
3.  Nel riquadro Espressione digitare l'espressione seguente:  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Per tutte le proprietà relative a Riempimento è necessario usare una stringa con il formato *nnyy*, dove *nn* è un numero e *yy* è l'unità di misura. L'espressione di esempio consente di compilare una stringa che utilizza la funzione **Level** per aumentare le dimensioni del riempimento in base al livello di ricorsione. A una riga di livello 1, ad esempio, verrà applicato un riempimento di (2 + (1\*10))=12pt e a una riga di livello 3 verrà applicato un riempimento di (2 + (3\*10))=32pt. Per informazioni sulla funzione **Level** , vedere [Livello](../../reporting-services/report-design/report-builder-functions-level-function.md).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Eseguire il report. Nel report viene visualizzata una vista gerarchica dei dati raggruppati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
