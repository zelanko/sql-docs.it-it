---
title: Creare un gruppo di gerarchie ricorsive (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5020b0d9dc509aff629347582ef1782d1262ceb8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041222"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>Creare un gruppo di gerarchie ricorsive (Generatore report e SSRS)
  In un gruppo di gerarchie ricorsive è possibile organizzare dati da un unico set di dati di un report in cui sono inclusi più livelli gerarchici, ad esempio il report per definire la struttura di relazioni tra dipendenti in una gerarchia organizzativa.  
  
 Prima che sia possibile organizzare i dati in una tabella come un gruppo di gerarchie ricorsive, è necessario disporre di un unico set di dati che contiene tutti i dati gerarchici. È necessario disporre di campi separati per gli elementi da raggruppare e per l'elemento in base al quale eseguire il raggruppamento. Un set di dati, ad esempio, in cui si desidera raggruppare i dipendenti in modo ricorsivo sotto il loro superiore, potrebbe contenere un nome, un nome di dipendente, un ID dipendente e un ID responsabile.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>Per creare un gruppo di gerarchie ricorsive  
  
1.  Nella visualizzazione della struttura aggiungere una tabella e trascinare i campi del set di dati da visualizzare. In genere, il campo che si desidera mostrare come una gerarchia si trova nella prima colonna.  
  
2.  Fare clic con il pulsante destro del mouse in un punto qualsiasi della tabella per selezionarla. Nel riquadro di raggruppamento viene visualizzato il gruppo di dettagli per la tabella selezionata. Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse su **Dettagli**, quindi scegliere **Modifica gruppo**. Verrà visualizzata la finestra di dialogo **Proprietà gruppo** .  
  
3.  In **Espressioni di raggruppamento**fare clic su **Aggiungi**. Nella griglia verrà visualizzata una nuova riga.  
  
4.  Nell'elenco **Raggruppa in base a** digitare o selezionare il campo da raggruppare.  
  
5.  Fare clic su **Avanzate**.  
  
6.  Nell'elenco **Elemento padre ricorsivo** immettere o selezionare il campo in base al quale eseguire il raggruppamento.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Eseguire il report. Nel report viene visualizzato il gruppo di gerarchie ricorsive, anche se non è presente alcun rientro per indicare la gerarchia.  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>Per formattare un gruppo di gerarchie ricorsive con livelli di rientro  
  
1.  Fare clic sulla casella di testo che contiene il campo cui si desidera aggiungere livelli di rientro per visualizzare un formato di gerarchia. Le proprietà per la casella di testo verranno visualizzate nel riquadro Proprietà.  
  
    > [!NOTE]  
    >  Se il riquadro Proprietà non è visualizzato, fare clic su **Proprietà** nella scheda **Visualizza** .  
  
2.  Nel riquadro Proprietà espandere la `Padding` nodo, fare clic su **a sinistra**e nell'elenco a discesa, selezionare  **\<espressione... >**.  
  
3.  Nel riquadro Espressione digitare l'espressione seguente:  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Per tutte le proprietà relative a Riempimento è necessario usare una stringa con il formato *nnyy*, dove *nn* è un numero e *yy* è l'unità di misura. L'espressione di esempio consente di compilare una stringa che utilizza la funzione `Level` per aumentare le dimensioni del riempimento in base al livello di ricorsione. A una riga di livello 1, ad esempio, verrà applicato un riempimento di (2 + (1\*10))=12pt e a una riga di livello 3 verrà applicato un riempimento di (2 + (3\*10))=32pt. Per informazioni sul `Level` funzione, vedere [livello](report-builder-functions-level-function.md).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Eseguire il report. Nel report viene visualizzata una vista gerarchica dei dati raggruppati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
