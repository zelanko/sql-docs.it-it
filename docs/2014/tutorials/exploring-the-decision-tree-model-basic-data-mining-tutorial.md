---
title: Esplorazione del modello di albero delle decisioni (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e7b77b445ff8cbef8be3acb72ef9cdb6fa3af159
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013742"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>Esplorazione del modello Decision Trees (Esercitazione di base sul data mining)
  L'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees consente di stimare quali colonne influiscono sulla decisione di acquistare una bicicletta in base alle colonne restanti nel set di training.  
  

  
##  <a name="Decision_Tree_Tab"></a> Scheda albero delle decisioni  
 Nel **albero delle decisioni** scheda, è possibile visualizzare gli alberi delle decisioni per ogni attributo stimabile nel set di dati.  
  
 In questo caso, il modello stima una sola colonna, ovvero Bike Buyer, pertanto non c'è un solo albero da visualizzare. Se si sono verificati più alberi, è possibile usare la **albero** casella per scegliere un altro albero.  
  
 Quando si visualizza il `TM_Decision_Tree` modello nel Visualizzatore albero delle decisioni, è possibile visualizzare gli attributi più importanti sul lato sinistro del grafico. "Più importanti" significa che questi attributi hanno la maggiore influenza sul risultato. Gli attributi nelle posizioni più basse dell'albero (a destra del grafico) hanno un minor effetto.  
  
 In questo esempio, l'età è il fattore più importante, nonché l'unico, nella stima dell'acquisto di biciclette. Il modello raggruppa i clienti in base all'età e quindi visualizza l'attributo più importante successivo per ogni fascia di età. Ad esempio, nel gruppo di clienti in età compresa tra 34 e 40 anni, il numero di automobili possedute è il criterio di stima più importante dopo l'età.  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>Per esplorare il modello nella scheda Albero delle decisioni  
  
1.  Selezionare il **visualizzatore modello di Data Mining** scheda **progettazione Data Mining**.  
  
     Per impostazione predefinita, verrà visualizzata la finestra di progettazione per il primo modello aggiunto alla struttura, in questo caso, `TM_Decision_Tree`.  
  
2.  Utilizzare i pulsanti a forma di lente di ingrandimento per regolare le dimensioni della visualizzazione dell'albero.  
  
     Per impostazione predefinita, nel Visualizzatore [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees vengono visualizzati solo i primi tre livelli dell'albero. Se l'albero contiene meno di tre livelli, il visualizzatore visualizza solo i livelli esistenti. È possibile visualizzare più livelli utilizzando il **Mostra il livello** dispositivo di scorrimento o il **espansione predefinita** elenco.  
  
3.  Diapositiva **Mostra il livello** fino alla quarta barra.  
  
4.  Modifica il **sfondo** valore `1`.  
  
     Modificando la **sfondo** impostazione, è possibile visualizzare rapidamente il numero di case in ogni nodo che presenta il valore di destinazione `1` per [Bike Buyer]. In questo particolare scenario ogni case rappresenta un cliente. Il valore `1` indica che il cliente ha già acquistato una bicicletta; il valore **0** indica che il cliente non ha acquistato una bicicletta. Quanto più scura appare l'ombreggiatura del nodo, tanto più alta sarà la percentuale di case nel nodo che presentano il valore di destinazione.  
  
5.  Posizionare il cursore sul nodo con l'etichetta **tutti**. Nella descrizione comando corrispondente verranno visualizzate le seguenti informazioni:  
  
    -   Numero totale di case  
  
    -   Numero di case relativi ai non acquirenti di biciclette  
  
    -   Numero di case relativi agli acquirenti di biciclette  
  
    -   Numero di case con valori mancanti per [Bike Buyer]  
  
     In alternativa, posizionare il cursore su un nodo qualsiasi dell'albero per visualizzare la condizione necessaria per raggiungere tale nodo dal nodo precedente. È anche possibile visualizzare queste stesse informazioni nel **legenda Data Mining**.  
  
6.  Fare clic sul nodo relativo **età > = 34 e < 41**. L'istogramma viene visualizzato come una barra orizzontale sottile sul nodo e rappresenta la distribuzione dei clienti in questa fascia di età che hanno (rosa) e non hanno acquistato (blu) una bicicletta. Il visualizzatore indica che i clienti di età compresa tra 34 e 40 anni non automuniti o proprietari di una sola auto acquisteranno probabilmente una bicicletta. È inoltre possibile constatare che la probabilità di acquistare una bicicletta aumenta se il cliente è di età compresa tra 38 e 40 anni.  
  
 Poiché al momento della creazione della struttura e del modello è stato abilitato il drill-through, è possibile recuperare informazioni dettagliate dai case del modello e dalla struttura di data mining, comprese le colonne non incluse nel modello di data mining (ad esempio emailAddress, FirstName).  
  
 Per altre informazioni, vedere [Query drill-through &#40;Data mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
#### <a name="to-drill-through-to-case-data"></a>Per eseguire il drill-through sui dati dei case  
  
1.  Fare doppio clic su un nodo e selezionare **drill-Through** quindi **solo colonne modello**.  
  
     I dettagli relativi a ogni case di training vengono visualizzati in formato foglio di calcolo. Tali dettagli provengono dalla vista vTargetMail selezionata come tabella del case durante la compilazione della struttura di data mining.  
  
2.  Fare doppio clic su un nodo e selezionare **drill-Through** quindi **colonne struttura e modello**.  
  
     Verrà visualizzato lo stesso foglio di calcolo con le colonne della struttura aggiunte alla fine.  
  
  
###  <a name="Dependency_Network_Tab"></a> Scheda rete di dipendenze  
 Il **rete di dipendenze** scheda vengono visualizzate le relazioni tra gli attributi che contribuiscono alla capacità predittiva del modello di data mining. Il Visualizzatore rete di dipendenze consolida il concetto dedotto dai risultati ottenuti, in base al quale l'età e l'area geografica sono fattori importanti nella stima dell'acquisto di biciclette.  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>Per esplorare il modello nella scheda Rete di dipendenze  
  
1.  Fare clic su di `Bike Buyer` nodo per identificarne le dipendenze.  
  
     Il nodo centrale per la rete di dipendenze, `Bike Buyer`, rappresenta l'attributo stimabile nel modello di data mining. Il grafico evidenzia tutti i nodi collegati che hanno un effetto sull'attributo stimabile.  
  
2.  Modificare il **tutti i collegamenti** dispositivo di scorrimento per identificare l'attributo più influente.  
  
     Quando si trascina il dispositivo di scorrimento verso il basso, gli attributi che hanno solo un effetto debole nella colonna [Bike Buyer] vengono rimossi dal grafico. Se si sposta il dispositivo di scorrimento è possibile verificare che l'età e l'area di residenza costituiscono i fattori principali per stimare se una persona è un acquirente di biciclette.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per esplorare i dati utilizzando gli altri tipi di modelli, vedere gli argomenti seguenti.  
  
-   [Esplorazione del modello di Clustering &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [Esplorazione del modello Naive Bayes &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello di Clustering &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al visualizzatore modello di data mining](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Scheda albero decisionale &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [Scheda rete di dipendenze &#40;visualizzatore modello di Data Mining&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [Visualizzare un modello usando il Visualizzatore Microsoft Decision Trees](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
