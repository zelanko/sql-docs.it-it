---
title: Creazione di una struttura del modello di data mining Sequence Clustering (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e9339227-6c2e-4c4b-8be2-8c1960bc4a8d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b7f4f543952fd86cf6c3c66f9f4b2c51019b1869
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63273483"
---
# <a name="creating-a-sequence-clustering-mining-model-structure-intermediate-data-mining-tutorial"></a>Creazione di una struttura del modello di data mining Sequence Clustering (Esercitazione intermedia sul data mining)
  Il primo passaggio nella creazione di un modello di data mining Sequence Clustering consiste nell'utilizzo della Creazione guidata modello di data mining per la creazione di una nuova struttura di data mining e di un modello di data mining sulla base dell'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
 Verrà utilizzata la stessa vista origine dati impiegata per l'analisi degli acquisti, ma si aggiungerà una colonna che contiene l'identificatore `sequence`. In questo scenario la sequenza indica l'ordine in cui il cliente ha incluso gli articoli tra gli acquisti.  
  
 Verranno anche aggiunte alcune colonne utilizzate in uno dei modelli per raggruppare i clienti in base ai dati demografici.  
  
### <a name="to-create-a-sequence-clustering-structure-and-model"></a>Per creare una struttura e un modello di data mining Sequence Clustering  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse su **strutture di data mining** e scegliere **nuova struttura di data mining**  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** verificare che sia selezionato **da database relazionale o data warehouse esistente** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Crea la struttura di data mining** verificare che sia selezionata l'opzione **crea struttura di data mining con un modello di data mining** . Quindi, fare clic sull'elenco a discesa dell'opzione **che data mining tecnica si desidera utilizzare**e selezionare **Microsoft Sequence Clustering**. Fare clic su **Avanti**.  
  
     Verrà visualizzata la pagina **Selezione vista origine dati** . In **viste origine dati disponibili**selezionare `Orders`.  
  
     Orders è la stessa vista origine dati utilizzata per lo scenario di analisi degli acquisti. Se questa vista origine dati non è stata creata, vedere [aggiunta di una vista origine dati con tabelle nidificate &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md).  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **impostazione tipi di tabelle** selezionare la casella di controllo **case** accanto alla tabella **vAssocSeqOrders** , quindi selezionare la casella di controllo **nidificata** accanto alla tabella **vAssocSeqLineItems** . Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  Se si verifica un errore quando si selezionano le caselle di controllo **case** o **nidificate** , è possibile che il join nella vista origine dati non sia corretto. La tabella nidificata, **vAssocSeqLineItems**, deve essere connessa alla tabella del case, **vAssocSeqOrders,** da un join molti-a-uno. È possibile modificare la relazione facendo clic con il pulsante destro del mouse sulla linea di join e invertendo la direzione del join. Per ulteriori informazioni, vedere finestra di [dialogo Crea relazione o modifica relazione &#40;Analysis Services-&#41;dati multidimensionali ](../../2014/analysis-services/create-or-edit-relationship-dialog-box-analysis-services-multidimensional-data.md).  
  
7.  Nella pagina **impostazione dati di training** scegliere le colonne da utilizzare nel modello selezionando una casella di controllo come segue:  
  
    -   **IncomeGroup** Selezionare la casella di controllo **input** .  
  
         Questa colonna contiene interessanti informazioni sui clienti che è possibile utilizzare per il clustering. Verranno utilizzate nel primo modello e ignorate nel secondo modello.  
  
    -   **OrderNumber** Selezionare la `Key` casella di controllo.  
  
         Questo campo sarà utilizzato come identificatore per la tabella del case o `Key`. In generale, è consigliabile non utilizzare mai il campo chiave della tabella del case come input, perché la chiave contiene valori univoci che non sono utili per il clustering.  
  
    -   **Area geografica** Selezionare la casella di controllo **input** .  
  
         Questa colonna contiene interessanti informazioni sui clienti che è possibile utilizzare per il clustering. Verranno utilizzate nel primo modello e ignorate nel secondo modello.  
  
    -   **LineNumber** Selezionare le `Key` caselle di controllo e **input** .  
  
         Il campo **lineNumber** verrà utilizzato come identificatore per la tabella nidificata o `Sequence Key`. La chiave di una tabella nidificata deve essere sempre utilizzata per l'input.  
  
    -   **Modello** di Selezionare le caselle di controllo **input** e **stimabile** .  
  
     Verificare che le selezioni siano corrette, quindi fare clic su **Avanti**.  
  
8.  Nella pagina **impostazione tipo di contenuto e dati delle colonne** verificare che la griglia contenga le colonne, i tipi di contenuto e i tipi di dati indicati nella tabella seguente, quindi fare clic su **Avanti**.  
  
    |Tabelle/Colonne|Content Type|Tipo di dati|  
    |---------------------|------------------|---------------|  
    |IncomeGroup|Discrete|Text|  
    |OrderNumber|Chiave|Text|  
    |Region|Discrete|Text|  
    |vAssocSeqLineItems|||  
    |Line Number|Key Sequence|long|  
    |Modello|Discrete|Text|  
  
9. Nella pagina **Crea set di testing** modificare la **percentuale di dati per il testing** su 20, quindi fare clic su **Avanti**.  
  
10. Nella pagina **Completamento procedura guidata** Digitare `Sequence Clustering with Region`per il **nome della struttura di data mining**.  
  
11. Per il **nome del modello di data mining**, digitare `Sequence Clustering with Region`.  
  
12. Selezionare la casella **Consenti drill-through** , quindi fare clic su **fine**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Elaborazione del modello Sequence Clustering](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione modelli di data mining](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Sequence Clustering](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)  
  
  
