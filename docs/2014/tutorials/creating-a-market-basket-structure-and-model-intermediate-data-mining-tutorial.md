---
title: Creazione di una struttura Market Basket e un modello (esercitazione intermedia di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190822"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello Market Basket (Esercitazione intermedia sul data mining)
  Dopo aver creato una vista origine dati, verrà utilizzata la Creazione guidata modello di data mining per creare una nuova struttura di data mining. In questa attività verranno creati una struttura di data mining e un modello di data mining basati sull'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
> [!NOTE]  
>  Se viene visualizzato un messaggio di errore che informa che non è possibile utilizzare vAssocSeqLineItems come tabella nidificata, tornare all'attività precedente della lezione e assicurarsi di creare il join molti-a-uno mediante trascinamento dalla tabella vAssocSeqLineItems (il lato "molti") alla tabella vAssocSeqOrders (il lato "uno"). È anche possibile modificare la relazione tra le tabelle facendo clic con il pulsante destro del mouse sulla linea join.  
  
### <a name="to-create-an-association-mining-structure"></a>Per creare una struttura di data mining di associazione  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], fare doppio clic su **strutture di Data Mining** e selezionare **nuova struttura di Data Mining** per aprire la procedura guidata di Data Mining dei dati.  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nel **Selezione metodo di definizione** verificare che **da esistenti database relazionale o data warehouse** sia selezionata e quindi fare clic su **Next**.  
  
4.  Nel **creare la struttura di Data Mining** nella pagina **tecnica di data mining si desidera utilizzare?** , selezionare **Microsoft Association Rules** dall'elenco, quindi fare clic su **Successivo**. Il **selezione vista origine dati** verrà visualizzata la pagina.  
  
5.  Selezionare **ordini**sotto **viste origine dati disponibili**, quindi fare clic su **Avanti**.  
  
6.  Nel **specificare i tipi di tabella** pagina, nella riga relativa alla tabella vAssocSeqLineItems, selezionare la **Nested** casella di controllo e nella riga per la tabella nidificata vAssocSeqOrders, selezionare il **Case** casella di controllo. Scegliere **Avanti**.  
  
7.  Nel **specificare i dati di Training** pagina, deselezionare le caselle che potrebbero essere archiviate. Impostare la chiave per la tabella del case, vAssocSeqOrders, selezionando il **chiave** casella di controllo accanto a OrderNumber.  
  
     Poiché lo scopo della market basket analysis è determinare quali prodotti sono inclusi in un'unica transazione, non è necessario usare il **CustomerKey** campo.  
  
8.  Impostare la chiave per la tabella nidificata, vAssocSeqLineItems, selezionando il **chiave** casella di controllo accanto al modello. Il **Input** casella di controllo è selezionata automaticamente anche quando si esegue questa operazione. Selezionare il **stimabile** casella di controllo per `Model` anche.  
  
     In un modello market basket, non si desidera eseguire sulla sequenza dei prodotti nel carrello acquisti e pertanto non è necessario includere **LineNumber** come chiave per la tabella nidificata. Si utilizzerebbe **LineNumber** come chiave solo in un modello in cui la sequenza è importante. Nella lezione 4 verrà creato un modello che utilizza l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Sequence Clustering.  
  
9. Selezionare la casella di controllo a sinistra delle colonne IncomeGroup e Region, ma non effettuare altre selezioni. Se si seleziona la colonna più a sinistra, verranno aggiunte le colonne alla struttura per riferimento futuro, ma non verranno utilizzate nel modello. Le selezioni effettuate dovrebbero corrispondere a quanto segue:  
  
     ![come dovrebbe apparire nella finestra di dialogo](../../2014/tutorials/media/tutorial-configassocmodel.gif "come dovrebbe apparire nella finestra di dialogo")  
  
10. Scegliere **Avanti**.  
  
11. Nel **contenuto e tipo di dati specificare colonne**pagina, rivedere le selezioni, che dovrebbero essere come illustrato nella tabella seguente e quindi fare clic su **successivo**.  
  
    |Colonne|Tipo di contenuto|Tipo di dati|  
    |-------------|------------------|---------------|  
    |IncomeGroup|Discrete|Testo|  
    |OrderNumber|Chiave|Testo|  
    |Region|Discrete|Testo|  
    |vAssocSeqLineItems|||  
    |Modello|Chiave|Testo|  
  
12. Nel **Create Test set** pagina, il valore predefinito per l'opzione **percentuale dei dati per i test** è 30 %). Impostare questa opzione su **0**. Scegliere **Avanti**.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce diversi grafici per misurare l'accuratezza del modello. Tuttavia, alcuni tipi di grafici di accuratezza, ad esempio il grafico di accuratezza e il report di convalida incrociata, sono progettati per l'esecuzione di classificazioni e stime. Non sono supportati per la stima associativa.  
  
13. Nel **Completamento procedura guidata** nella pagina **nome struttura di Data Mining**, tipo `Association`.  
  
14. Nelle **nome del modello di Data Mining**, tipo `Association`.  
  
15. Selezionare l'opzione **Consenti drill-through**, quindi fare clic su **fine**.  
  
     Verrà aperto Progettazione modelli di Data Mining per visualizzare il `Association` struttura di data mining appena creato.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica ed elaborazione del modello Market Basket &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Association Rules](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Tipi di contenuto &#40;Data mining&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  
