---
title: Aggiunta di una vista origine dati con tabelle nidificate (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a14cd7f1-7a10-4ec6-af6a-f5f0676a0308
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 648b9d561ae340b67ed5e2d1aa878969e5a3bc47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822779"
---
# <a name="adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial"></a>Aggiunta di una vista origine dati con tabelle nidificate (Esercitazione intermedia sul data mining)
  Per creare un modello di analisi degli acquisti, è necessario utilizzare una vista origine dati che supporti dati associativi. Questa vista origine dati verrà utilizzata anche per lo scenario di clustering delle sequenze.  
  
 Questa vista origine dati è diversa da altre che potrebbero essere state elaborate perché contiene una *tabella nidificata*. Una *tabella nidificata* è una tabella che contiene più righe di informazioni su una singola riga della tabella del case. Se ad esempio il modello analizza il comportamento di acquisto dei clienti, in genere si utilizza una tabella che dispone di una riga univoca per ogni cliente come tabella del case. Ogni cliente potrebbe tuttavia fare più acquisti, pertanto potrebbe essere necessario analizzare la sequenza di prodotti che vengono frequentemente acquistati insieme. Per rappresentare in modo logico questi acquisti nel modello, è necessario aggiungere un'altra tabella alla vista origine dati che elenca gli acquisti per ogni cliente.  
  
 La tabella degli acquisti nidificata è correlata alla tabella dei clienti con una relazione molti-a-uno. La tabella nidificata potrebbe contenere molte righe per ogni cliente, ognuna delle quali contiene un solo prodotto acquistato, con informazioni aggiuntive sull'ordine tramite il quale sono stati effettuati gli acquisti, il prezzo al momento dell'ordine o eventuali promozioni applicate. È possibile utilizzare le informazioni nella tabella nidificata come input per il modello o come attributo stimabile.  
  
 In questa lezione verranno effettuate le operazioni seguenti:  
  
-   Si aggiunge una vista origine dati all'origine [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] dati.  
  
-   Si aggiungeranno il case e le tabelle nidificate alla vista aggiunta.  
  
-   Si specificherà la relazione molti-a-uno tra il case e la tabella nidificata.  
  
    > [!NOTE]  
    >  . È importante attenersi con scrupolo alla procedura descritta per specificare correttamente la relazione tra la tabella del case e la tabella nidificata ed evitare errori quando si elabora il modello.  
  
-   Si definirà in che modo vengono utilizzate le colonne di dati nel modello.  
  
 Per ulteriori informazioni sull'utilizzo delle tabelle case e nidificate e su come scegliere una chiave di tabella nidificata, vedere [tabelle nidificate &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md).  
  
### <a name="to-add-a-data-source-view"></a>Per aggiungere una vista origine dati  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **viste origine dati**, quindi scegliere **nuova vista origine dati**.  
  
     Verrà avviata Creazione guidata vista origine dati.  
  
2.  Nella pagina **Creazione guidata vista origine dati** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione origine dati** , in **origini dati relazionali**, selezionare l' [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origine dati creata nell'esercitazione di base sul data mining. Fare clic su **Avanti**.  
  
4.  Nella pagina **Selezione tabelle e viste** selezionare le tabelle seguenti, quindi fare clic sulla freccia destra per includerle nella nuova vista origine dati:  
  
    -   `vAssocSeqOrders`  
  
    -   `vAssocSeqLineItems`  
  
5.  Fare clic su **Avanti**.  
  
6.  Per impostazione predefinita, nella pagina **Completamento procedura guidata** la vista origine dati è denominata [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Modificare il nome in `Orders`, quindi fare clic su **fine**.  
  
     Verrà aperto Progettazione vista origine dati e `Orders` verrà visualizzata la vista origine dati.  
  
### <a name="to-create-a-relationship-between-tables"></a>Per creare una relazione tra le tabelle  
  
1.  In Progettazione vista origine dati posizionare le due tabelle in modo che siano allineate orizzontalmente, con la tabella vAssocSeqLineItems sulla sinistra e la tabella vAssocSeqOrders sulla destra.  
  
2.  Selezionare la colonna **OrderNumber** nella tabella vAssocSeqLineItems.  
  
3.  Trascinare la colonna nella tabella vAssocSeqOrders e inserirla nella colonna **OrderNumber** .  
  
    > [!IMPORTANT]  
    >  Assicurarsi di trascinare la colonna **OrderNumber** dalla tabella nidificata vAssocSeqLineItems, che rappresenta il lato molti del join, alla tabella del case vAssocSeqOrders, che rappresenta il lato uno del join.  
  
     Esiste ora una nuova *relazione molti-a-uno* tra le tabelle VAssocSeqLineItems e vAssocSeqOrders. Se le tabelle sono state unite in join correttamente, la vista origine dati visualizzata sarà simile alla seguente:  
  
     ![Join molti-a-uno previsto in una tabella del case e in una tabella nidificata](../../2014/tutorials/media/dsv-nestedjoin-illustration.gif "Join molti-a-uno previsto in una tabella del case e in una tabella nidificata")  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di una struttura e di un modello di Market basket &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelli di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
