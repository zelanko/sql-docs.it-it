---
title: Creazione di una struttura e di un modello Market Basket (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 207d82f740b7b5ff174e220e647d67d5bac7f9ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63190822"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello Market Basket (Esercitazione intermedia sul data mining)
  Dopo aver creato una vista origine dati, verrà utilizzata la Creazione guidata modello di data mining per creare una nuova struttura di data mining. In questa attività verranno creati una struttura di data mining e un modello di data mining basati sull'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
> [!NOTE]  
>  Se viene visualizzato un messaggio di errore che informa che non è possibile utilizzare vAssocSeqLineItems come tabella nidificata, tornare all'attività precedente della lezione e assicurarsi di creare il join molti-a-uno mediante trascinamento dalla tabella vAssocSeqLineItems (il lato "molti") alla tabella vAssocSeqOrders (il lato "uno"). È anche possibile modificare la relazione tra le tabelle facendo clic con il pulsante destro del mouse sulla linea join.  
  
### <a name="to-create-an-association-mining-structure"></a>Per creare una struttura di data mining di associazione  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse su **strutture di data** mining e scegliere **nuova struttura di data** mining per aprire Creazione guidata modello di data mining  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** verificare che sia selezionato **da database relazionale o data warehouse esistente** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Crea la struttura di data mining** in **cui data mining tecnica si desidera utilizzare?** selezionare **Microsoft Association Rules** dall'elenco e quindi fare clic su **Avanti**. Verrà visualizzata la pagina **Selezione vista origine dati** .  
  
5.  Selezionare **Orders**in **viste origine dati disponibili**, quindi fare clic su **Avanti**.  
  
6.  Nella pagina **impostazione tipi di tabelle** , nella riga relativa alla tabella vAssocSeqLineItems, selezionare la casella di controllo **nidificata** , quindi nella riga relativa alla tabella nidificata vAssocSeqOrders selezionare la casella di controllo **case** . Fare clic su **Avanti**.  
  
7.  Nella pagina **impostazione dati di training** deselezionare le caselle che potrebbero essere selezionate. Impostare la chiave per la tabella del case, vAssocSeqOrders, selezionando la casella di controllo **chiave** accanto a OrderNumber.  
  
     Poiché lo scopo del Market basket analysis è determinare quali prodotti sono inclusi in una singola transazione, non è necessario utilizzare il campo **CustomerKey** .  
  
8.  Impostare la chiave per la tabella nidificata, vAssocSeqLineItems, selezionando la casella di controllo **chiave** accanto a modello. Quando si esegue questa operazione, viene automaticamente selezionata anche la casella di controllo **input** . Selezionare anche la casella di `Model` controllo **stimabile** .  
  
     In un modello Market basket, non si è interessati alla sequenza di prodotti nel carrello acquisti e pertanto non è necessario includere **lineNumber** come chiave per la tabella nidificata. È possibile utilizzare **lineNumber** come chiave solo in un modello in cui la sequenza è importante. Nella lezione 4 verrà creato un modello che utilizza l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
9. Selezionare la casella di controllo a sinistra delle colonne IncomeGroup e Region, ma non effettuare altre selezioni. Se si seleziona la colonna più a sinistra, verranno aggiunte le colonne alla struttura per riferimento futuro, ma non verranno utilizzate nel modello. Le selezioni effettuate dovrebbero corrispondere a quanto segue:  
  
     ![Aspetto della finestra di dialogo](../../2014/tutorials/media/tutorial-configassocmodel.gif "Aspetto della finestra di dialogo")  
  
10. Fare clic su **Avanti**.  
  
11. Nella pagina **impostazione tipo di contenuto e dati delle colonne**esaminare le selezioni, che devono essere come illustrato nella tabella seguente, quindi fare clic su **Avanti**.  
  
    |Colonne|Content Type|Tipo di dati|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|Testo|  
    |Order Number|Chiave|Testo|  
    |Region|Discrete|Testo|  
    |vAssocSeqLineItems|||  
    |Modello|Chiave|Testo|  
  
12. Nella pagina **Crea set di testing** il valore predefinito per l'opzione **percentuale di dati per il testing** è il 30%. Modificare in **0**. Fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce diversi grafici per misurare l'accuratezza del modello. Tuttavia, alcuni tipi di grafici di accuratezza, ad esempio il grafico di accuratezza e il report di convalida incrociata, sono progettati per l'esecuzione di classificazioni e stime. Non sono supportati per la stima associativa.  
  
13. Nella pagina **Completamento procedura guidata** Digitare `Association`in **Nome struttura di data mining**.  
  
14. In **nome modello di data mining**Digitare `Association`.  
  
15. Selezionare l'opzione **Consenti drill-through**, quindi fare clic su **fine**.  
  
     Progettazione modelli di data mining viene aperto `Association` per visualizzare la struttura di data mining appena creata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica ed elaborazione del modello Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Algoritmo Microsoft Association](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipi di contenuto &#40;Data mining&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
