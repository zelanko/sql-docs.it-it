---
title: Filtro di una tabella nidificata in un modello di data mining (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f57d691587d658e968cd79cf4f4ab4731db29915
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63267475"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>Applicazione di filtri a una tabella nidificata in un modello di data mining (Esercitazione intermedia sul data mining)
  Dopo avere creato ed esplorato il modello, si decide che si desidera concentrarsi su un subset dei dati sui clienti. Potrebbe ad esempio essere necessario analizzare solo gli acquisti relativi a uno specifico articolo o analizzare i dati demografici dei clienti che non hanno effettuato acquisti in un determinato periodo.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] consente di filtrare i dati utilizzati in un modello di data mining. Questa funzionalità è utile perché non è necessario configurare una nuova vista origine dati per l'utilizzo di dati diversi. Nell'esercitazione di base sul data mining è stato descritto come filtrare i dati da una tabella flat applicando condizioni alla tabella del case. In questa attività verrà creato un filtro che si applica a una tabella nidificata.  
  
## <a name="filters-on-nested-vs-case-tables"></a>Filtri su tabelle nidificate o tabelle del case  
 Se la vista origine dati contiene una tabella del case e una tabella nidificata, come la vista origine dati utilizzata nel modello di associazione, è possibile applicare filtri in base ai valori nella tabella del case, alla presenza o assenza di un valore nella tabella nidificata o a una combinazione di entrambi.  
  
 In questa attività verrà innanzitutto creata una copia del modello di associazione, quindi si aggiungeranno gli attributi IncomeGroup e Region al nuovo modello correlato, in modo da applicare filtri in base a tali attributi nella tabella del case.  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>Per creare e modificare una copia del modello di associazione  
  
1.  Nella scheda **modelli di data mining** di fare clic con il `Association` pulsante destro del mouse sul modello e scegliere [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] **nuovo modello di data mining**.  
  
2.  Per **nome modello**, digitare `Association Filtered`. Per **Nome algoritmo**selezionare **Microsoft Association Rules**. Fare clic su **OK**.  
  
3.  Nella colonna per il modello Association Filtered fare clic sulla riga IncomeGroup e modificare il valore da **Ignore** a **input**.  
  
 Il passaggio successivo consiste nella creazione di un filtro sulla tabella del case nel nuovo modello di associazione. Il filtro passerà al modello solo i clienti nell'area di destinazione o con il livello di reddito di destinazione. Si aggiungerà quindi un secondo set di condizioni di filtro per specificare che il modello utilizza solo i clienti i cui acquisti contengono almeno un articolo.  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>Per aggiungere un filtro a un modello di data mining  
  
1.  Nella scheda **modelli di data mining** fare clic con il pulsante destro del mouse sull'associazione di modelli filtrata e selezionare **Imposta filtro modello**.  
  
2.  Nella finestra di dialogo **Filtro modello** fare clic sulla riga superiore nella griglia della casella di testo **Colonna struttura di data mining** .  
  
3.  Nella casella di testo **colonna struttura di data mining** selezionare IncomeGroup.  
  
     L'icona a sinistra della casella di testo cambia per indicare che l'elemento selezionato è una colonna.  
  
4.  Fare clic sulla casella di testo **operatore** e **=** Selezionare l'operatore nell'elenco.  
  
5.  Fare clic sulla casella di testo **valore** e `High` digitare nella casella.  
  
6.  Fare clic sulla riga successiva nella griglia.  
  
7.  Fare clic sulla casella di testo **and/or** nella riga successiva della griglia e selezionare **o**.  
  
8.  Nella casella di testo **colonna struttura di data mining** selezionare IncomeGroup. Nella casella di testo **valore** Digitare `Moderate`.  
  
     La condizione di filtro creata viene aggiunta automaticamente alla casella di testo **espressione** e dovrebbe apparire come segue:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. Fare clic sulla riga successiva nella griglia, lasciando l'operatore come predefinito, **e**.  
  
10. Per **operator**, lasciare il valore predefinito, **Contains**. Fare clic sulla casella di testo **valore** .  
  
11. Nella finestra di dialogo **filtro** , nella prima riga sotto **colonna struttura di data mining**Selezionare `Model`.  
  
12. Per **operator**selezionare **is not null**. Lasciare vuota la casella di testo **valore** . Fare clic su **OK**.  
  
     La condizione di filtro nella casella di testo **espressione** della finestra di dialogo **filtro modello** viene aggiornata automaticamente per includere la nuova condizione nella tabella nidificata. L'espressione completa è la seguente:  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>Per abilitare il drill-through ed elaborare il modello filtrato  
  
1.  Nella scheda **modelli di data mining** fare clic con il `Association Filtered` pulsante destro del mouse sul modello e scegliere **proprietà**.  
  
2.  Modificare la proprietà **AllowDrillThrough** in **true**.  
  
3.  Fare clic con il `Association Filtered` pulsante destro del mouse sul modello di data mining e scegliere **Elabora modello**.  
  
4.  Fare clic su **Sì** nel messaggio di errore per distribuire il nuovo modello [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel database.  
  
5.  Nella finestra di dialogo **Elabora struttura di data mining** fare clic su **Esegui**.  
  
6.  Al termine dell'elaborazione, fare clic su **Chiudi** per uscire dalla finestra di dialogo **stato** elaborazione, quindi fare di nuovo clic su **Chiudi** per chiudere la finestra di dialogo **Elabora struttura di data mining** .  
  
 È possibile verificare tramite Microsoft Generic Content Tree Viewer e controllando il valore di NODE_SUPPORT che il modello filtrato contenga meno case del modello originale.  
  
## <a name="remarks"></a>Osservazioni  
 Il filtro della tabella nidificata che è stato creato controlla solo la presenza di almeno una riga nella tabella nidificata, tuttavia è anche possibile creare condizioni di filtro che verifichino la presenza di prodotti specifici.  È ad esempio possibile creare il filtro seguente:  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 Questa istruzione indica che i clienti della tabella del case devono essere limitati a quelli che hanno acquistato una bottiglia d'acqua (Water Bottle). Tuttavia, poiché il numero di attributi della tabella nidificata è potenzialmente illimitato, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non viene fornito un elenco di valori possibili da cui effettuare una selezione. È invece necessario digitare il valore esatto.  
  
 È possibile fare clic su **modifica query** per modificare manualmente l'espressione di filtro. Se tuttavia si modifica manualmente una parte di un'espressione di filtro, la griglia verrà disabilitata e da allora in poi sarà necessario utilizzare l'espressione di filtro solo in modalità di modifica di testo. Per ripristinare la modalità di modifica della griglia, è necessario cancellare l'espressione di filtro e ricominciare.  
  
> [!WARNING]  
>  Non è possibile utilizzare l'operatore LIKE nel filtro di una tabella nidificata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Stima delle associazioni &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Sintassi del filtro del modello ed esempi &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
