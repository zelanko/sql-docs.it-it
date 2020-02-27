---
title: Aggiungere o eliminare un gruppo in un'area dati (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4de53c3c-c6fc-49ce-b692-3609fc0b3ec5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e559dc00246fb0b990c81de99c8036356a64034f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081582"
---
# <a name="add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs"></a>Aggiunta o eliminazione di un gruppo in un'area dati (Generatore report e SSRS)
Nei report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è possibile aggiungere un gruppo a un'area dati quando si desidera organizzare i dati in base a un valore o a un set di espressioni specifico per la visualizzazione e i calcoli. A un gruppo sono associati un nome e un'espressione che consentono di identificare quali dati di un set di dati appartengono al gruppo. Per altre informazioni sui gruppi, vedere [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
 In un'area dati Tablix fare clic nella tabella, nella matrice o nell'elenco per visualizzare il riquadro di raggruppamento. Trascinare i campi del set di dati nel riquadro Gruppo di righe e Gruppo di colonne per creare gruppi padre o gruppi figlio. Fare clic con il pulsante destro del mouse su un gruppo esistente per aggiungere un gruppo adiacente. Per definizione, il gruppo di dettagli è il gruppo più interno e può essere aggiunto solo come gruppo figlio. Fare clic con il pulsante destro del mouse su un gruppo esistente per eliminarlo. Verranno aggiunte automaticamente righe e colonne nelle quali è possibile visualizzare valori di gruppo. Per altre informazioni, vedere [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
 In un'area dati del grafico fare clic nel grafico per visualizzare le aree di rilascio. Creare gruppi trascinando campi del set di dati nelle aree di rilascio dei campi categoria e serie. Per aggiungere gruppi nidificati, aggiungere più campi all'area di rilascio.  
  
 Per impostazione predefinita, i gruppi non sono definiti in un misuratore. Il comportamento predefinito per il misuratore è aggregare tutti i valori nel campo specificato in un unico valore visualizzato sul misuratore. Per altre informazioni, vedere [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-parent-or-child-row-or-column-group-to-a-tablix-data-region"></a>Per aggiungere un gruppo di righe o di colonne padre o figlio a un'area dati Tablix  
  
1.  Trascinare un campo dal riquadro **Dati report** nel riquadro **Gruppi di righe** o nel riquadro **Gruppi di colonne** .  
  
    > [!NOTE]  
    >  Se il riquadro Raggruppamento non è visualizzato, scegliere **Raggruppamento**dalla scheda Visualizza.  
  
2.  Rilasciare il campo al di sopra o al di sotto della gerarchia di gruppi utilizzando la barra della guida per posizionare il gruppo come gruppo padre o gruppo figlio di un gruppo esistente.  
  
     Il gruppo verrà aggiunto con un nome, un'espressione di raggruppamento e un'espressione di ordinamento predefiniti che si basano sul nome del campo.  
  
## <a name="to-add-an-adjacent-row-or-column-group-to-a-tablix-data-region"></a>Per aggiungere un gruppo di righe o di colonne adiacenti a un'area dati Tablix  
  
1.  Nel riquadro di raggruppamento fare clic con il pulsante destro del mouse su un gruppo di livello pari a quello che si desidera aggiungere. Fare clic su **Aggiungi gruppo**, quindi su **Adiacente prima** o su **Adiacente dopo** per specificare dove aggiungere il gruppo. Verrà visualizzata la finestra di dialogo **Gruppo Tablix** .  
  
2.  Nella casella **Nome**digitare un nome per il gruppo.  
  
3.  In **Espressione di raggruppamento**digitare un'espressione o fare clic sul pulsante espressione (**fx**) per creare un'espressione.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Vengono aggiunti un nuovo gruppo al riquadro di raggruppamento e una riga o una colonna nelle quali visualizzare valori di gruppo all'area dati Tablix nell'area di progettazione.  
  
## <a name="to-add-a-details-group-to-a-tablix-data-region"></a>Per aggiungere un gruppo dettagli a un'area dati Tablix  
  
1.  Nel riquadro di raggruppamento fare clic con il pulsante destro del mouse sul gruppo figlio più interno, escluso il gruppo **Dettagli** . Scegliere **Aggiungi gruppo**, quindi fare clic su **Gruppo figlio**. Verrà visualizzata la finestra di dialogo **Gruppo Tablix** .  
  
2.  In **Espressione di raggruppamento**lasciare vuota l'espressione. In un gruppo dettagli non è presente alcuna espressione.  
  
3.  Selezionare **Mostra dati dettaglio**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Un nuovo gruppo dettagli verrà aggiunto come gruppo figlio nel riquadro di raggruppamento e nell'handle di riga per il gruppo selezionato al passaggio 1 verrà visualizzata l'icona del gruppo dettagli. Per altre informazioni sugli handle, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
## <a name="to-edit-a-row-or-column-group-in-a-tablix-data-region"></a>Per modificare un gruppo di righe o di colonne in un'area dati Tablix  
  
1.  Nell'area di progettazione del report fare clic in un punto qualsiasi dell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne.  
  
2.  Fare clic con il pulsante destro del mouse sul gruppo e scegliere **Proprietà gruppo**.  
  
3.  Nella casella **Nome**digitare il nome del gruppo.  
  
4.  In **Espressioni di raggruppamento**digitare o selezionare un'espressione semplice o fare clic sul pulsante Espressione (**fx**) per creare un'espressione di raggruppamento.  
  
5.  Fare clic su **Aggiungi** per creare altre espressioni. Tutte le espressioni specificate vengono combinate mediante un operatore logico AND in modo da specificare i dati per questo gruppo.  
  
6.  (Facoltativo) Fare clic su **Interruzioni di pagina** per impostare le opzioni relative alle interruzioni di pagina.  
  
7.  (Facoltativo) Fare clic su **Ordinamento** per selezionare o digitare espressioni che specificano l'ordinamento per i valori del gruppo.  
  
8.  (Facoltativo) Fare clic su **Visibilità** per selezionare le opzioni di visibilità per l'elemento.  
  
9. (Facoltativo) Fare clic su **Filtri** per impostare i filtri per questo gruppo.  
  
10. (Facoltativo) Fare clic su **Variabili** per definire variabili che hanno come ambito questo gruppo e che sono accessibili da qualsiasi gruppo figlio.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-group-from-a-tablix-data-region"></a>Per eliminare un gruppo da un'area dati Tablix  
  
1.  Nel riquadro Raggruppamento fare clic con il pulsante destro del mouse sul gruppo e scegliere **Elimina gruppo**.  
  
2.  Nella finestra di dialogo **Elimina gruppo** selezionare una delle opzioni seguenti:  
  
    -   **Elimina gruppo e righe e colonne correlate** Scegliere questa opzione per eliminare la definizione di gruppo e tutte le righe correlate in cui sono visualizzati i dati di gruppo. Per il gruppo dettagli, se la stessa riga appartiene sia ai dati di dettaglio che a quelli di gruppo, verranno eliminate solo le righe dei dati di dettaglio.  
  
    -   **Elimina solo gruppo** Scegliere questa opzione per mantenere inalterata la struttura dell'area dati Tablix ed eliminare solo la definizione del gruppo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-delete-a-details-group-from-a-tablix-data-region"></a>Per eliminare un gruppo dettagli da un'area dati Tablix  
  
1.  Nel riquadro Raggruppamento fare clic con il pulsante destro del mouse sul gruppo dettagli e scegliere **Elimina gruppo**.  
  
2.  Nella finestra di dialogo **Elimina gruppo** selezionare una delle opzioni seguenti:  
  
    -   **Elimina gruppo e righe e colonne correlate** Scegliere questa opzione per eliminare la definizione di gruppo e tutte le righe correlate in cui sono visualizzati i dati di gruppo. Per il gruppo dettagli, se la stessa riga appartiene sia ai dati di dettaglio che a quelli di gruppo, verranno eliminate solo le righe dei dati di dettaglio.  
  
    -   **Elimina solo gruppo** Scegliere questa opzione per mantenere inalterata la struttura dell'area dati Tablix ed eliminare solo la definizione del gruppo.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Il gruppo dettagli verrà eliminato.  
  
    > [!NOTE]  
    >  Verificare che dopo avere rimosso una riga di dettaglio l'espressione in ogni cella specifichi un'espressione di aggregazione laddove appropriato. Se necessario, modificare l'espressione in modo da specificare funzioni di aggregazione in base alle necessità.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti a raccolte di variabili di report e di gruppo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
