---
title: Aggiungere un ordinamento interattivo a una tabella o a una matrice (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10121"
- sql13.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2b2cb0ecbaf608a1dd7b11d610321fbc7e943334
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65582002"
---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>Aggiungere un ordinamento interattivo a una tabella o a una matrice (Generatore report e SSRS)
  È possibile aggiungere pulsanti di ordinamento interattivo per consentire agli utenti di modificare l'ordinamento di righe e colonne in tabelle e matrici. Questa caratteristica è disponibile solo nei formati di rendering che supportano l'interazione dell'utente, ad esempio HTML.  
  
 Quando si crea un pulsante di ordinamento interattivo, è necessario specificare gli elementi da ordinare, l'elemento in base al quale eseguire l'ordinamento e l'ambito al quale applicare l'ordinamento. È ad esempio possibile ordinare le righe di dettaglio in base al cognome del cliente, i valori di gruppi di sottocategorie all'interno di un gruppo di categorie in base alle vendite o i valori combinati di gruppi di categorie e di sottocategorie in base ai totali.  
  
 Quando si visualizza il report, le colonne che supportano l'ordinamento interattivo presentano icone a forma di freccia che assumono un aspetto differente per indicare l'ordinamento. La prima volta che si fa clic su un pulsante di ordinamento interattivo, gli elementi vengono disposti in ordine crescente. Facendo clic successivamente sarà possibile alternare l'ordinamento crescente e quello decrescente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="BackToTop"></a> Contenuto dell'articolo  
 [Ordinamento delle righe di dettaglio di una tabella senza gruppi](#SortingDetailRows)  
  
 [Ordinamento di un gruppo di righe padre di livello principale di una tabella o di una matrice](#SortingTopLevelParent)  
  
 [Ordinamento dei gruppi figlio o delle righe di dettaglio di un gruppo](#SortingChildGroups)  
  
 [Ordinamento di righe in base a un'espressione di raggruppamento complessa](#SortingMultipleRowGroups)  
  
 [Sincronizzazione dell'ordinamento per più aree dati](#SynchronizingSortOrder)  
  
##  <a name="SortingDetailRows"></a> Ordinamento delle righe di dettaglio di una tabella senza gruppi  
 Aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna in modo che gli utenti possano fare clic su tale intestazione per ordinare le righe di dettaglio in una tabella in base al valore visualizzato nella colonna.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>Per aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna per ordinare la tabella in base a un valore  
  
1.  In una tabella senza gruppi nella visualizzazione di progettazione del report fare clic con il pulsante destro del mouse nella casella di testo dell'intestazione di colonna alla quale si vuole aggiungere un pulsante di ordinamento interattivo e quindi scegliere **Proprietà casella di testo**.  
  
2.  Fare clic su **Ordinamento interattivo**.  
  
3.  Selezionare **Abilita ordinamento interattivo a questa casella di testo**.  
  
4.  In **Scegli gli elementi da ordinare**fare clic su **Righe di dettaglio**.  
  
5.  In **Ordina per**specificare un'espressione di ordinamento. Dall'elenco a discesa selezionare il campo corrispondente alla colonna per la quale si sta definendo un'azione di ordinamento. Per un'intestazione di colonna denominata "Title", scegliere ad esempio `[Title]`. È obbligatorio specificare un'espressione di ordinamento.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Ripetere i passaggi da 1 a 6 per ogni colonna alla quale si desidera aggiungere un pulsante di ordinamento interattivo.  
  
 Per verificare l'azione di ordinamento, fare clic su **Esegui** per visualizzare l'anteprima del report e fare clic sul pulsante di ordinamento interattivo.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="SortingTopLevelParent"></a> Ordinamento di un gruppo di righe padre di livello principale di una tabella o di una matrice  
 Aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna in modo che gli utenti possano fare clic su tale intestazione per ordinare le righe del gruppo padre in una tabella o in una matrice in base al valore visualizzato nella colonna. L'ordine dei gruppi figlio rimane invariato.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>Per aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna per ordinare i gruppi  
  
1.  In una tabella o in una matrice nella visualizzazione di progettazione del report fare clic con il pulsante destro del mouse nella casella di testo dell'intestazione di colonna del gruppo al quale si vuole aggiungere un pulsante di ordinamento interattivo e quindi scegliere **Proprietà casella di testo**.  
  
2.  Fare clic su **Ordinamento interattivo**.  
  
3.  Selezionare **Abilita ordinamento interattivo a questa casella di testo**.  
  
4.  In **Scegli gli elementi da ordinare**fare clic su **Gruppi**.  
  
5.  Nell'elenco a discesa selezionare il nome del gruppo che si sta ordinando. Per i gruppi basati su espressioni di raggruppamento semplici, il valore **Ordina per** viene popolato con un'espressione di raggruppamento.  
  
    > [!NOTE]  
    >  Per espressioni di raggruppamento complesse, impostare manualmente l'espressione **Ordina per** sullo stesso valore dell'espressione di raggruppamento.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Per verificare l'azione di ordinamento, fare clic su **Esegui** per visualizzare l'anteprima del report e fare clic sul pulsante di ordinamento interattivo.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="SortingChildGroups"></a> Ordinamento dei gruppi figlio o delle righe di dettaglio di un gruppo  
 Aggiungere un pulsante di ordinamento interattivo a una riga di intestazione di gruppo in modo che gli utenti possano ordinare i valori di un gruppo figlio da un gruppo padre o ordinare le righe di dettaglio per il gruppo figlio più interno.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>Per aggiungere un pulsante di ordinamento interattivo a una casella di testo in un'intestazione di riga di gruppo per ordinare gruppi figlio o righe di dettaglio  
  
1.  Nella visualizzazione di progettazione del report fare clic con il pulsante destro del mouse nella casella di testo della riga di intestazione di gruppo alla quale si vuole aggiungere un pulsante di ordinamento interattivo e quindi scegliere **Proprietà casella di testo**.  
  
2.  Fare clic su **Ordinamento interattivo**.  
  
3.  Selezionare **Abilita ordinamento interattivo a questa casella di testo**.  
  
4.  In **Scegli gli elementi da ordinare**fare clic su una delle opzioni seguenti:  
  
    -   **Dettagli** Fare clic su **Dettagli** per ordinare le righe di dettaglio. Nell'elenco a discesa selezionare il campo in base al quale eseguire l'ordinamento. Per questa opzione è necessario specificare il valore in base al quale eseguire l'ordinamento.  
  
    -   **Gruppi** Fare clic su **Gruppi** per ordinare i valori dei gruppi figlio. Per questa opzione, l'espressione **ordina per** viene compilata automaticamente dall'espressione di raggruppamento.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Per verificare l'azione di ordinamento, fare clic su **Esegui** per visualizzare l'anteprima del report e fare clic sul pulsante di ordinamento interattivo.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="SortingMultipleRowGroups"></a> Ordinamento di righe in base a un'espressione di raggruppamento complessa  
 Aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna in modo che gli utenti possano fare clic su tale intestazione per ordinare gruppi padre e figlio combinati. Per ottenere questo risultato, è necessario modificare l'espressione di raggruppamento in modo che rappresenti una combinazione di entrambi i gruppi. Si supponga, ad esempio, che una matrice visualizzi i totali delle scorte di un negozio per determinati elementi raggruppati per colore e dimensioni. Per ordinare le righe in base alla combinazione di colore e dimensioni, anziché creare un gruppo distinto per ognuna di queste proprietà, è possibile definire un gruppo basato su tale combinazione. Per altre informazioni sulla definizione delle espressioni di raggruppamento, vedere [Esempi di espressioni di raggruppamento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md).  
  
 I termini nella procedura seguente specificano aree dell'area dati Tablix. Per altre informazioni, vedere [Aree dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-areas-report-builder-and-ssrs.md).  
  
 In genere quando si ordinano le righe in base a più gruppi, si desidera in genere visualizzare i totali delle righe ordinate, indipendentemente dai gruppi di colonne. In questa procedura non vengono utilizzati gruppi di colonne. Per iniziare, si aggiunge una matrice e si rimuove il gruppo di colonne predefinito. In alternativa, è possibile iniziare aggiungendo una tabella e rimuovendo il gruppo dettagli.  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>Per aggiungere un pulsante di ordinamento interattivo a un'intestazione di colonna per ordinare più gruppi  
  
1.  Aggiungere una matrice nella visualizzazione di progettazione del report.  
  
2.  Trascinare un campo numerico nella cella di dati per collegare il set di dati alla matrice.  
  
     Procedere quindi alla creazione di un gruppo con un'espressione di raggruppamento che specifichi più campi e un'intestazione di gruppo da utilizzare per visualizzare i valori di gruppo.  
  
3.  Verificare che la matrice sia selezionata nell'area di progettazione. Nel riquadro Raggruppamento verrà visualizzato un gruppo di righe e di colonne predefinito.  
  
4.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul gruppo di righe predefinito, quindi scegliere **Modifica gruppo**. Verrà visualizzata la finestra di dialogo **Proprietà gruppo** .  
  
5.  Nella casella **Nome**sostituire il nome predefinito con un nome che specifichi più gruppi in base ai quali si vuole eseguire il raggruppamento.  
  
6.  In **Raggruppa in base a**di **Espressioni di raggruppamento**fare clic sul pulsante Espressione (**fx**) per aprire la finestra di dialogo **Espressione** .  
  
7.  Digitare l'espressione che specifica tutti i campi in base ai quali si desidera eseguire il raggruppamento. Nell'espressione di raggruppamento seguente vengono, ad esempio, combinati i campi denominati Color (Colore) e Size (Dimensioni): `=Fields!Color.Value & Fields!Size.Value`.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     La definizione del gruppo è stata completata. Procedere quindi trascinando i campi da visualizzare nell'area del corpo della Tablix della matrice. Aggiungere all'area del corpo della Tablix i campi in base ai quali si è scelto di eseguire il raggruppamento nel passaggio 7, ognuno nella rispettiva colonna.  
  
     Per questo scenario non è necessaria la prima colonna nell'area dei gruppi di righe della Tablix. Per eliminare la colonna, fare clic con il pulsante destro del mouse sull'intestazione di colonna e quindi scegliere **Elimina colonne**. Verrà visualizzata una finestra di dialogo in cui viene richiesto se si desidera procedere all'eliminazione dei gruppi associati. Fare clic su **No**. L'area dei gruppi di righe verrà eliminata e rimarrà solo l'area del corpo della Tablix.  
  
     Procedere quindi alla rimozione del gruppo di colonne predefinito.  
  
9. Nel riquadro Gruppi di colonne fare clic con il pulsante destro del mouse sul gruppo di colonne predefinito e quindi scegliere **Elimina gruppo**. Verrà visualizzata una finestra di dialogo in cui viene richiesto se si desidera eliminare il gruppo con le righe e le colonne correlate o solo il gruppo. Fare clic su **Elimina solo gruppo**. Il gruppo di colonne verrà eliminato insieme alla relativa area e rimarrà solo l'area del corpo della Tablix.  
  
     Procedere quindi all'aggiunta di un pulsante di ordinamento interattivo alla casella di testo che include la matrice.  
  
10. Fare clic nella casella di testo nella prima riga e selezionare **Proprietà casella di testo**.  
  
11. Fare clic su **Ordinamento interattivo**.  
  
12. Selezionare **Abilita ordinamento interattivo a questa casella di testo**.  
  
13. In **Scegli gli elementi da ordinare**fare clic su **Gruppi**.  
  
14. Nell'elenco a discesa selezionare il nome del gruppo creato nel passaggio 5. L'espressione di raggruppamento verrà copiata automaticamente nella casella di testo **Ordina per** .  
  
15. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Con questa procedura si è aggiunto il pulsante di ordinamento alla casella di testo.  
  
16. (Facoltativo) È possibile eliminare i valori duplicati nelle colonne contenenti valori di gruppo. Nell'area di progettazione del report fare clic sulla casella di testo contenente il valore per il quale si desidera nascondere i valori ripetuti. Nel riquadro Proprietà scorrere fino a **HideDuplicates**e selezionare il nome del set di dati collegato a questa matrice nell'elenco a discesa.  
  
 Per verificare l'azione di ordinamento, fare clic su **Esegui** per visualizzare l'anteprima del report e fare clic sul pulsante di ordinamento interattivo. La matrice viene ordinata in base ai valori combinati dell'espressione di raggruppamento, anche se ogni singolo valore viene visualizzato nella rispettiva colonna.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
##  <a name="SynchronizingSortOrder"></a> Sincronizzazione dell'ordinamento per più aree dati  
 Aggiungere un pulsante di ordinamento interattivo in modo che gli utenti possano fare clic su di esso per ordinare più aree dati. Quando si crea un pulsante di ordinamento interattivo, è possibile specificare se sincronizzare l'ordinamento per più aree dati in base allo stesso set di dati del report. Un report può, ad esempio, includere una matrice e un grafico in cui i dati sono rappresentati in forma grafica. Quando un utente modifica l'ordinamento delle righe nella matrice, nel grafico viene automaticamente visualizzato lo stesso ordinamento.  
  
 Per sincronizzare l'ordinamento, è necessario utilizzare espressioni di ordinamento identiche per le aree dati o per i gruppi da ordinare, nonché definire l'ambito dell'ordinamento in modo che rappresenti un predecessore comune a entrambe le aree dati. Il predecessore comune può essere il set di dati al quale vengono collegate entrambe le aree dati o un'area dati contenitore all'interno della quale sono incluse entrambe le aree dati. Si supponga, ad esempio, che un report includa sia una matrice che un grafico in cui sono visualizzati dati provenienti dallo stesso set di dati, all'interno di un elenco. Per sincronizzare l'azione di ordinamento, è necessario specificare l'ordinamento interattivo in una colonna della matrice e impostare l'ambito sull'elenco. Quando l'utente ordina la matrice, viene ordinato anche il grafico.  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>Per sincronizzare l'ordinamento con un grafico per un pulsante di ordinamento interattivo in un'area dati della matrice  
  
1.  Aggiungere una matrice al report nella relativa visualizzazione di progettazione.  
  
2.  Aggiungere un campo del set di dati numerico alla cella di dati della matrice, ad esempio un campo che rappresenta quantità o vendite.  
  
3.  Definire un gruppo di righe. Per impostazione predefinita, l'ordinamento per il gruppo viene impostato su un'espressione identica a quella di raggruppamento.  
  
4.  Aggiungere un grafico al report, ad esempio un grafico a torta.  
  
5.  Trascinare il campo scelto nel passaggio 2 nell'area **Valore** del riquadro **Dati grafico** .  
  
6.  Trascinare il campo scelto per il raggruppamento nell'area **Gruppi di categorie** .  
  
     L'espressione di raggruppamento per il gruppo di righe della matrice deve essere identica a quella per il gruppo di categorie del grafico.  
  
7.  Fare clic con il pulsante destro del mouse sul gruppo di categorie e quindi scegliere **Proprietà gruppo categorie**.  
  
8.  Fare clic su **Ordinamento**.  
  
9. Scegliere **Aggiungi**. Nella griglia delle opzioni di ordinamento verrà aggiunta una nuova riga di ordinamento.  
  
10. Nell'elenco a discesa dell'opzione Ordina per scegliere lo stesso campo selezionato nel passaggio 6 per il raggruppamento.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
12. Nella matrice fare clic con il pulsante destro del mouse nella casella di testo dell'intestazione di colonna alla quale si vuole aggiungere un pulsante di ordinamento interattivo e quindi scegliere **Proprietà casella di testo**.  
  
13. Fare clic su **Ordinamento interattivo**.  
  
14. Selezionare **Abilita ordinamento interattivo a questa casella di testo**.  
  
15. In **Scegli gli elementi da ordinare**fare clic su **Gruppi**.  
  
16. Dall'elenco a discesa disponibile in **Gruppi**selezionare il nome del gruppo che si sta ordinando. Per il valore **Ordina per** verrà automaticamente impostata l'espressione di raggruppamento per questo gruppo.  
  
17. Selezionare **Applica questo ordinamento ad altri gruppi o aree dati in**. Nella casella di testo digitare il nome del set di dati, ad esempio "Dati vendite".  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Per verificare l'azione di ordinamento, fare clic su **Esegui** per visualizzare l'anteprima del report e fare clic sul pulsante di ordinamento interattivo. La matrice viene ordinata in base ai valori combinati dell'espressione di raggruppamento, anche se ogni singolo valore viene visualizzato nella rispettiva colonna.  
  
 ![Icona freccia usata con il collegamento Torna all'inizio](../../analysis-services/instances/media/uparrow16x16.gif "Icona freccia usata con il collegamento Torna all'inizio") [Torna all'inizio](#BackToTop)  
  
## <a name="see-also"></a>Vedere anche  
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Ordinamento interattivo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md)   
 [Ordinamento dei dati in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Esplorazione della flessibilità di un'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
