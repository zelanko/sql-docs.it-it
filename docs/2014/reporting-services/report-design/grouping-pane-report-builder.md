---
title: Riquadro di raggruppamento (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8f04df51d1a88ac0fb13ce1a262b3e3ebc245004
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953167"
---
# <a name="grouping-pane-report-builder"></a>Riquadro di raggruppamento (Generatore report)
  Nel riquadro Raggruppamento vengono visualizzati i gruppi di righe e di colonne dell'area dati Tablix selezionata. Il riquadro Raggruppamento non è disponibile per le aree dati Grafico e Misuratore. Il riquadro Raggruppamento è costituito da un riquadro Gruppi di righe e da un riquadro Gruppi di colonne e include due modalità: predefinita e avanzata. Nella modalità predefinita è riportata una visualizzazione gerarchica dei membri dinamici dei gruppi di righe e di colonne. Nella modalità avanzata vengono visualizzati sia i membri dinamici che quelli statici dei gruppi di righe e di colonne. Un gruppo è un set di dati denominato che deriva da un set di dati del report visualizzato in un'area dati. I gruppi sono organizzati in gerarchie che includono membri statici e dinamici. Per altre informazioni, vedere [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Se non viene visualizzato il riquadro Raggruppamento, scegliere **Mostra/Nascondi** dal menu **Visualizza**e fare clic su **Raggruppamento**.  
  
 Le celle nelle aree dei gruppi di colonne e di righe possono essere membri statici o dinamici di un gruppo di righe o di colonne Tablix. I membri statici vengono ripetuti una volta per ogni gruppo e in genere contengono etichette o totali. I membri dinamici vengono ripetuti una volta per ogni istanza di gruppo e in genere contengono i valori univoci dell'espressione di raggruppamento. Quando si selezionano celle della Tablix nell'area dei gruppi di righe o di colonne, viene selezionato il membro di gruppo corrispondente nel riquadro Gruppi di righe o Gruppi di colonne. Viceversa, se si selezionano gruppi nel riquadro di raggruppamento, la cella corrispondente associata al membro del gruppo viene selezionata nell'area di progettazione. Per altre informazioni sulle aree dei gruppi di colonne e righe Tablix, vedere [Aree dell'area dati Tablix &#40;Generatore report e SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 Il riquadro di raggruppamento supporta le modalità seguenti:  
  
-   **Valore predefinito.** Utilizzare la modalità predefinita per aggiungere, modificare o eliminare gruppi. È possibile aggiungere gruppi padre, figlio e gruppi di dettagli trascinando campi dal riquadro dei dati del report e inserendoli nella gerarchia dei gruppi. Per aggiungere un gruppo adiacente, è necessario usare il collegamento **Aggiungi gruppo** . Per altre informazioni, vedere [Aggiunta o eliminazione di un gruppo in un'area dati &#40;Generatore report e SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
-   **Avanzate**. Usare la **Modalità avanzata** per visualizzare tutti i membri dei gruppi di righe e di colonne e per impostare le proprietà sui membri statici. Quando si creano gruppi o si aggiungono totali, vengono impostate automaticamente le proprietà che controllano il rendering delle righe e delle colonne in ogni pagina del report nell'area dati Tablix. Per regolare manualmente queste proprietà, è necessario impostarle sul membro Tablix. Per altre informazioni, vedere [Controllo della visualizzazione dell'area dati Tablix in una pagina del report &#40;Generatore report e SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
## <a name="default-mode"></a>Modalità predefinita  
 Quando è attiva la modalità predefinita, nei riquadri Gruppi di righe e Gruppi di colonne è riportata una visualizzazione gerarchica di tutti i gruppi padre, i gruppi figlio e i gruppi adiacenti. Un gruppo figlio viene visualizzato in posizione rientrata rispetto al gruppo padre. Un gruppo adiacente viene visualizzato allo stesso livello di rientro dei gruppi di pari livello. Nella figura seguente viene illustrata un'area dati Tablix con gruppi di righe nidificati e gruppi di colonne nidificati e adiacenti.  
  
 ![Tablix, gruppi di righe e colonne annidate e adiacenti](../media/rs-basictablixdesigngroupingpane.gif "Tablix, gruppi di righe e colonne annidate e adiacenti")  
  
 Nel riquadro di raggruppamento vengono visualizzati i gruppi di righe e di colonne corrispondenti. Nella figura seguente sono stati selezionati il gruppo basato sulla sottocategoria nel riquadro Gruppi di righe e la cella di raggruppamento [Subcat] nell'area dati Tablix:  
  
 ![Riquadro di raggruppamento per gruppi di righe e colonne annidate](../media/rs-basictablixdesigngroupingpanedefaultview.gif "Riquadro di raggruppamento per gruppi di righe e colonne annidate")  
  
 Nel riquadro Gruppi di righe il gruppo basato sulla sottocategoria è un figlio del gruppo basato sulla categoria. Nel riquadro Gruppi di colonne il gruppo Country/Region è un figlio del gruppo Geography. Il gruppo Year e i gruppi Country/Region sono gruppi adiacenti.  
  
 Per altre informazioni, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="advanced-mode"></a>Modalità avanzata  
 Quando è attiva la modalità avanzata, i riquadri Gruppi di righe e Gruppi di colonne contengono una vista gerarchica di tutti i gruppi, inclusi i membri statici e dinamici. Quando si seleziona un membro, nel riquadro delle proprietà vengono visualizzate le proprietà per il membro Tablix selezionato.  
  
> [!NOTE]  
>  Per attivare/disattivare la **Modalità avanzata**fare clic con il pulsante destro del mouse sulla freccia Giù accanto al riquadro Gruppi di colonne, quindi scegliere **Modalità avanzata**.  
  
 Nella maggior parte dei casi, le proprietà che controllano la visualizzazione delle righe e delle colonne di gruppo statiche e dinamiche vengono impostate automaticamente al momento della creazione di un gruppo o dell'aggiunta dei totali. Per modificare i valori predefiniti, è necessario selezionare il membro di gruppo nel riquadro Gruppi di righe o Gruppi di colonne e modificare i valori delle proprietà nella finestra Proprietà. Sono disponibili le proprietà seguenti:  
  
-   **FixedData**. Proprietà di tipo Boolean. valida per le intestazioni di riga e di colonna esterne. Consente di bloccare l'area dei gruppi di righe durante lo scorrimento verticale o l'area dei gruppi di colonne durante lo scorrimento orizzontale in un renderer quale HTML.  
  
-   **HideIfNoRows**. Proprietà di tipo Boolean. valida solo per i membri statici. Se questa proprietà è impostata, Hidden e ToggleItem vengono ignorate. Consente di nascondere il membro se l'area dati Tablix non contiene le righe dei dati.  
  
-   **KeepTogether**. Proprietà di tipo Boolean. Indica se i membri dell'intera area dati Tablix e gli eventuali membri nidificati devono essere mantenuti insieme in un'unica pagina, se possibile.  
  
-   `KeepWithGroup` (Indici per tabelle con ottimizzazione per la memoria). Proprietà di tipo Boolean. Valida solo per i membri di riga statici. Se possibile, consente di mantenere la riga con il membro dinamico di pari livello precedente o successivo, se non è nascosto. Per mantenere l'intestazione di una riga con il gruppo associato, impostare KeepWithGroup su **After**.  
  
-   `RepeatOnNewPage` (Indici per tabelle con ottimizzazione per la memoria). Proprietà di tipo Boolean. Valida solo per i membri di riga statici e quando la proprietà KeepWithGroup non è impostata su None. Se possibile, ripetere questa riga statica in ogni pagina contenente almeno un'istanza del membro dinamico specificato da KeepWithGroup. Per mantenere l'intestazione di una riga con il gruppo associato, impostare RepeatOnNewPage su **True**.  
  
-   `Hidden` (Indici per tabelle con ottimizzazione per la memoria). Proprietà di tipo Boolean. Indica se è necessario nascondere inizialmente la riga o la colonna.  
  
-   **ToggleItem.** Stringa. Il nome della casella di testo alla quale aggiungere l'immagine dell'elemento Toggle. La casella di testo deve trovarsi nello stesso ambito del gruppo o in un ambito contenitore.  
  
 Per altre informazioni, vedere [Controllo della visualizzazione dell'area dati Tablix in una pagina del report &#40;Generatore report e SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md), [Visualizzare intestazioni e piè di pagina con un gruppo &#40;Generatore report e SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md), e [Visualizzare le intestazioni di riga e colonna in più pagine &#40;Generatore report e SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Non tutti i membri statici dispongono di un'intestazione che corrisponde a una cella nell'area di progettazione. Nel riquadro di raggruppamento la convenzione seguente indica se un membro statico non dispone di intestazione:  
  
-   **Statico** Indica un membro statico con una cella di intestazione.  
  
-   **(Statico)** Indica un membro statico senza cella di intestazione, noto come statico nascosto.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
