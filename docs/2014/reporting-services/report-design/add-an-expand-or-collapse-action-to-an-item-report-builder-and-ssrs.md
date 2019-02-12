---
title: Aggiungere un'azione Espandi o Comprimi a un elemento (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 49f07ad6-242b-4861-8fc1-91ca78c36d6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 21726a3f57db48a9dd1ec163de7ece3ba5e544c4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56037780"
---
# <a name="add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs"></a>Aggiungere un'azione Espandi o Comprimi a un elemento (Generatore report e SSRS)
  È possibile permettere a un utente di espandere o comprimere in modo interattivo elementi del report oppure, per una tabella o una matrice, righe e colonne associate a un gruppo. Per consentire agli utenti di espandere o comprimere un elemento, impostare le proprietà di visibilità per tale elemento. L'impostazione della visibilità può essere usata in un visualizzatore di report HTML ed è a volte definita azione *drill-down* .  
  
 Nella visualizzazione di progettazione report specificare il nome della casella di testo del report in cui si desidera espandere e comprimere le icone degli elementi Toggle. Nella casella di testo del report visualizzabile vengono visualizzati, oltre al contenuto, un segno più (+) o un segno meno (-). Quando l'utente fa clic sull'elemento Toggle, la visualizzazione del report viene aggiornata per visualizzare o nascondere l'elemento del report, in base alle impostazioni di visibilità correnti per gli elementi presenti nel report.  
  
 In genere, l'azione di espansione e compressione viene utilizzata per visualizzare inizialmente solo dati di riepilogo e per consentire all'utente di fare clic sul segno più per visualizzare i dati di dettaglio. È possibile, ad esempio, nascondere inizialmente una tabella in cui sono visualizzati valori per un grafico oppure nascondere gruppi figlio per una tabella con gruppi di righe o di colonne annidati, come in un report drill-down.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-expand-and-collapse-action-to-a-group"></a>Per aggiungere a un gruppo un'azione per espandere e comprimere  
  
1.  Nella visualizzazione di progettazione report fare clic sulla tabella o sulla matrice per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne.  
  
     ![Riquadro di raggruppamento](../media/groupingpane.png "Riquadro di raggruppamento")  
  
     Se il riquadro di raggruppamento non è visualizzato, scegliere **Raggruppamento** dal menu **Visualizza**.  
  
2.  Fare clic con il pulsante destro del mouse in un punto qualsiasi sulla barra del titolo del riquadro di raggruppamento e scegliere **Avanzate**. La modalità del riquadro di raggruppamento viene attivata/disattivata per mostrare la struttura di visualizzazione sottostante per righe e colonne nell'area di progettazione.  
  
     ![Riquadro di raggruppamento con menu Modalità avanzata](../media/groupingpane-advancedmode.png "Riquadro di raggruppamento con menu Modalità avanzata")  
  
3.  Nel riquadro di gruppo appropriato fare clic sul nome del gruppo di righe o del gruppo di colonne per il quale si desidera nascondere le righe o le colonne associate. Il gruppo viene selezionato e nel riquadro Proprietà vengono visualizzate le proprietà **Membro Tablix** .  
  
    > [!NOTE]  
    >  Se il riquadro Proprietà non è visualizzato, fare clic su **Visualizza** sulla barra multifunzione e quindi su **Proprietà**.  
  
4.  In `Hidden`, scegliere una delle opzioni seguenti per impostare la visibilità di questo elemento del report la prima volta che si esegue un report:  
  
    -   Selezionare `False` per visualizzare l'elemento del report.  
  
    -   Selezionare `True` per nascondere l'elemento del report.  
  
    -   Selezionare **\<Espressione>** per aprire la finestra di dialogo **Espressione** nella quale è possibile creare un'espressione che viene valutata in fase di runtime per determinare la visibilità.  
  
5.  Nella casella a discesa in **ToggleItem**selezionare il nome di una casella di testo alla quale aggiungere l'immagine dell'elemento Toggle.  
  
     Nella figura seguente il gruppo Colora riga è configurato per permettere agli utenti a espandere e comprimere le righe associate.  
  
     ![Configurazione di un gruppo di righe da espandere](../media/expandcollapse-confighiddentoggleitemwithnumbers.png "Configurazione di un gruppo di righe da espandere")  
  
    > [!NOTE]  
    >  La casella di testo con l'immagine dell'elemento Toggle non può essere il gruppo di righe o colonne per il quale si desidera nascondere le righe o le colonne associate. Deve trovarsi nello stesso gruppo dell'elemento che viene nascosto o in un gruppo predecessore. Ad esempio, per attivare/disattivare la visibilità di righe associate a un gruppo figlio, selezionare una casella di testo in una riga associata al gruppo padre.  
  
6.  Per testare l'elemento Toggle, eseguire il report e fare clic sulla casella di testo con l'immagine dell'elemento Toggle. La visualizzazione del report viene aggiornata per mostrare i gruppi di righe e di colonne con la rispettiva visibilità attivata/disattivata.  
  
     ![Esecuzione di report con gruppo di righe espandibile](../media/expandcollapse-runreport-rowgroup.png "Esecuzione di report con gruppo di righe espandibile")  
  
### <a name="to-add-expand-and-collapse-action-to-a-report-item"></a>Per aggiungere a un elemento del report un'azione per espandere e comprimere  
  
1.  Nella visualizzazione di progettazione report fare clic con il pulsante destro del mouse sull'elemento del report da visualizzare o nascondere e scegliere **Proprietà** *\<elemento report*. Viene visualizzata la finestra di dialogo **Proprietà** *\<elemento report>* relativa all'elemento report.  
  
2.  Fare clic su **Visibilità**.  
  
3.  In **Quando il report viene eseguito inizialmente**scegliere una delle opzioni seguenti per impostare la visibilità di questo elemento del report la prima volta che si esegue un report:  
  
    -   Selezionare **Mostra** per visualizzare l'elemento del report.  
  
    -   Selezionare **Nascondi** per nascondere l'elemento del report.  
  
    -   Selezionare **Mostra o nascondi in base a un'espressione** per determinare la visibilità usando un'espressione valutata in fase di runtime. Fare clic su (**fx**) per aprire la finestra di dialogo **Espressione** per creare un'espressione.  
  
        > [!NOTE]  
        >  Quando si specifica un'espressione per la visibilità, viene impostata la proprietà Hidden dell'elemento di report. L'espressione restituisce un valore `Boolean` `True` per nascondere l'elemento e `False` per visualizzarlo.  
  
4.  Nella casella a discesa di **La visualizzazione può essere attivata/disattivata tramite questo elemento del report**selezionare il nome di una casella di testo nel report nella quale visualizzare l'immagine di un elemento Toggle, ad esempio Textbox1.  
  
     Nella figura seguente la tabella è configurata per permettere agli utenti di espanderla e comprimerla. La visualizzazione della tabella è attivata e disattivata dalla casella di testo della tabella Products.  
  
     ![Configurare una tabella del report da espandere](../media/expandcollapse-reporttable.png "Configurare una tabella del report da espandere")  
  
    > [!NOTE]  
    >  La casella di testo utilizzata per l'elemento Toggle deve trovarsi nell'ambito corrente o contenitore di questo elemento di report (tale da includere il corpo del report). Ad esempio, per attivare/disattivare la visibilità di un grafico, selezionare una casella di testo che si trovi nello stesso ambito contenitore del grafico, ad esempio il corpo del report o un rettangolo. La casella di testo deve trovarsi nella stessa gerarchia del contenitore o a un livello superiore.  
  
5.  Per testare l'elemento Toggle, eseguire il report e fare clic sulla casella di testo con l'immagine dell'elemento Toggle. La visualizzazione del report viene aggiornata per mostrare gli elementi del report con la rispettiva visibilità attivata/disattivata.  
  
     ![Esecuzione di report con tabella di espansione](../media/expandcollapse-runreport-reporttable.png "Esecuzione di report con tabella di espansione")  
  
## <a name="see-also"></a>Vedere anche  
 [Azione di drill-down &#40;Generatore report e SSRS &#41;](drilldown-action-report-builder-and-ssrs.md)   
 [Nascondere un elemento &#40;Generatore report e SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
