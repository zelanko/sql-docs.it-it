---
title: Creazione di una struttura di rete neurale e di un modello (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62856317"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello di rete neurale (Esercitazione intermedia sul data mining)
  Per creare un modello di data mining, è innanzitutto necessario utilizzare la Creazione guidata modello di data mining per creare una nuova struttura di data mining basata sulla nuova vista origine dati. In questa attività verrà utilizzata la procedura guidata per creare una struttura di data mining e, contemporaneamente, il modello di data mining associato basato sull'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Neural Network.  
  
 Poiché le reti neurali sono estremamente flessibili e possono analizzare molte combinazioni di input e output, è necessario sperimentare diverse modalità di elaborazione dei dati per ottenere risultati ottimali. Potrebbe ad esempio, si desidera personalizzare il modo in cui l'obiettivo numerico per la qualità del servizio viene *binned*, o raggruppati per soddisfare requisiti aziendali specifici. A tale scopo, è necessario aggiungere una nuova colonna alla struttura di data mining per raggruppare i dati numerici in modi diversi, quindi creare un modello che utilizzi la nuova colonna. Questi modelli di data mining verranno utilizzati per alcune attività di esplorazione.  
  
 Dopo avere identificato, grazie al modello di rete neurale, i fattori di maggiore impatto per le questioni aziendali, sarà infine necessario compilare un modello distinto per la stima e l'assegnazione dei punteggi. Verrà utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Logistic Regression, basato sul modello di rete neurale, ma ottimizzato per la ricerca di una soluzione basata su input specifici.  
  
 **Passaggi**  
  
 [Creare la struttura di data mining predefinito e il modello](#bkmk_defaul)  
  
 [Utilizzare la discretizzazione per categorizzare la colonna stimabile](#bkmk_ColumnCopy)  
  
 [Copiare la colonna e modificare il metodo di discretizzazione per un altro modello](#bkmk_Alias)  
  
 [Creare un alias per la colonna stimabile in modo che sia possibile confrontare i modelli](#bkmk_Alias2)  
  
 [Elaborare tutti i modelli](#bkmk_SeedProcess)  
  
## Creare la struttura predefinita del Call Center  <a name="bkmk_defaul"></a>  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], fare doppio clic su **strutture di Data Mining** e selezionare **nuova struttura di Data Mining**.  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nel **Selezione metodo di definizione** verificare che **da esistenti database relazionale o data warehouse** sia selezionata e quindi fare clic su **Next**.  
  
4.  Nel **creare la struttura di Data Mining** verificare che l'opzione **Crea struttura di data mining con un modello di data mining** sia selezionata.  
  
5.  Fare clic sull'elenco a discesa per l'opzione **tecnica di data mining si desidera utilizzare?** , quindi selezionare **Microsoft Neural Network**.  
  
     Poiché i modelli di regressione logistica sono basati sulle reti neurali, è possibile riutilizzare la stessa struttura e aggiungere un nuovo modello di data mining.  
  
6.  Scegliere **Avanti**.  
  
     Il **selezione vista origine dati** verrà visualizzata la pagina.  
  
7.  Sotto **viste origine dati disponibili**, selezionare `Call Center`, fare clic su **successivo**.  
  
8.  Nel **specificare i tipi di tabella** pagina, selezionare la **Case** casella di controllo accanto al **FactCallCenter** tabella. Non si seleziona alcun valore per **DimDate**. Scegliere **Avanti**.  
  
9. Nel **specificare i dati di Training** pagina, selezionare **chiave** accanto alla colonna **FactCallCenterID.**  
  
10. Selezionare il `Predict` e **Input** caselle di controllo.  
  
11. Selezionare il **Key**, **Input**, e `Predict` caselle di controllo come illustrato nella tabella seguente:  
  
    |Tabelle/Colonne|Chiave/Input/Stima|  
    |---------------------|-------------------------|  
    |AutomaticResponses|Input|  
    |AverageTimePerIssue|Input/Stima|  
    |Calls|Input|  
    |DateKey|Non utilizzare|  
    |DayOfWeek|Input|  
    |FactCallCenterID|Chiave|  
    |IssuesRaised|Input|  
    |LevelOneOperators|Input/Stima|  
    |LevelTwoOperators|Input|  
    |Orders|Input/Stima|  
    |ServiceGrade|Input/Stima|  
    |Turno|Input|  
    |TotalOperators|Non utilizzare|  
    |WageType|Input|  
  
     Notare che sono state selezionate più colonne stimabili. Uno degli aspetti positivi dell'algoritmo Neural Network è la capacità di analizzare tutte le possibili combinazioni di attributi di input e output. È preferibile non eseguire questa operazione per grandi set di dati, come può aumentare in modo esponenziale il tempo di elaborazione...  
  
12. Nel **contenuto e tipo di dati specificare colonne** pagina, verificare che la griglia contenga le colonne, i tipi di contenuto e i tipi di dati come illustrato nella tabella seguente e quindi fare clic su **successivo**.  
  
    |Colonne|Tipo di contenuto|Tipi di dati|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|Continuo|Long|  
    |AverageTimePerIssue|Continuo|Long|  
    |Calls|Continuo|Long|  
    |DayOfWeek|Discrete|Testo|  
    |FactCallCenterID|Chiave|Long|  
    |IssuesRaised|Continuo|Long|  
    |LevelOneOperators|Continuo|Long|  
    |LevelTwoOperators|Continuo|Long|  
    |Orders|Continuo|Long|  
    |ServiceGrade|Continuo|Double|  
    |Turno|Discrete|Testo|  
    |WageType|Discrete|Testo|  
  
13. Nel **Create Test set** pagina, deselezionare la casella di testo per l'opzione **percentuale dei dati per i test**. Scegliere **Avanti**.  
  
14. Nel **Completamento procedura guidata** pagina, per il **nome struttura di Data Mining**, tipo `Call Center`.  
  
15. Per il **nome del modello di Data Mining**, tipo `Call Center Default NN`, quindi fare clic su **fine**.  
  
     Il **Consenti drill-through** finestra è disabilitata perché è impossibile il drill-through ai dati con modelli di rete neurale.  
  
16. In Esplora soluzioni fare doppio clic il nome della struttura di data mining appena creato e selezionare **processo**.  
  
## <a name="use-discretization-to-bin-the-target-column"></a>Utilizzare la discretizzazione per categorizzare la colonna di destinazione  
 Per impostazione predefinita, quando si crea un modello di rete neurale che include un attributo stimabile numerico, tramite l'algoritmo Microsoft Neural Network l'attributo viene considerato come un numero continuo. L'attributo ServiceGrade, ad esempio, è un numero che teoricamente varia da 0,00 (risposta a tutte le chiamate) a 1,00 (tutti i chiamanti riattaccano). In questo set di dati i valori hanno la distribuzione seguente:  
  
 ![distribuzione dei valori del livello servizio](../../2014/tutorials/media/skt-service-grade-valuesc.gif "distribuzione dei valori del livello servizio")  
  
 Di conseguenza, quando si elabora il modello, gli output possono essere raggruppati in modo diverso dal previsto. Ad esempio, se si usa il clustering per identificare i gruppi di procedure di valori, l'algoritmo divide i valori di ServiceGrade in intervalli come questo: 0.0748051948 - 0.09716216215. Benché questo raggruppamento sia matematicamente preciso, gli intervalli potrebbero non essere altrettanto significativi per gli utenti aziendali.  
  
 In questo passaggio per rendere più intuitiva, il risultato si raggrupperanno i valori numerici in modo diverso, la creazione di copie della colonna di dati numerici.  
  
### <a name="how-discretization-works"></a>Funzionamento della discretizzazione  
 Analysis Services offre un'ampia gamma di metodi per suddividere in contenitori o elaborare dati numerici. Nella tabella seguente vengono illustrate le differenze tra i risultati quando l'attributo di output ServiceGrade viene elaborato in tre modi diversi, ovvero:  
  
-   Considerandolo un numero continuo.  
  
-   Lasciando che l'algoritmo utilizzi il clustering per identificare la migliore disposizione di valori.  
  
-   Specificando che i numeri siano inseriti in contenitori in base al metodo delle aree uguali,  
  
 Modello predefinito (continuo)  
  
|Value|SUPPORT|  
|-----------|-------------|  
|Missing|0|  
|0.09875|120|  
  
 Suddiviso tramite clustering  
  
|Value|SUPPORT|  
|-----------|-------------|  
|\< 0.0748051948|34|  
|0.0748051948 - 0.09716216215|27|  
|0.09716216215 - 0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 Suddiviso in base al metodo delle aree uguali  
  
|Value|SUPPORT|  
|-----------|-------------|  
|\< 0.07|26|  
|0.07 - 0.00|22|  
|0.09 - 0.11|36|  
|>= 0.12|36|  
  
> [!NOTE]  
>  È possibile ottenere tali statistiche dal nodo delle statistiche marginali del modello al termine dell'elaborazione di tutti i dati. Per altre informazioni sul nodo delle statistiche marginali, vedere [modello di contenuto di Data Mining per i modelli di rete neurale &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 Nella colonna VALUE di questa tabella è indicato come è stato gestito il numero per ServiceGrade. Nella colonna SUPPORT è indicato quanti case avevano tale valore o rientravano in tale intervallo.  
  
-   **Utilizzare numeri continui (impostazione predefinita)**  
  
     Se è stato utilizzato il metodo predefinito, l'algoritmo calcolerà i risultati per 120 valori distinti, il cui valore medio è 0,09875. È inoltre possibile visualizzare il numero di valori mancanti.  
  
-   **Suddividere tramite clustering**  
  
     Quando si consente all'algoritmo Microsoft Clustering di determinare il raggruppamento facoltativo dei valori, i valori per ServiceGrade verranno raggruppati in cinque (5) intervalli. Il numero di case in ogni intervallo non viene distribuito uniformemente, come si vedere nella colonna Support.  
  
-   **Suddividere tramite aree uguali**  
  
     Quando si sceglie questo metodo, l'algoritmo forza i valori in bucket di uguale dimensione che a loro volta modificano i limiti superiori e inferiori di ogni intervallo. È possibile specificare il numero di bucket, ma è consigliabile evitare di avere bucket contenenti solo pochi valori.  
  
 Per altre informazioni sulla creazione di contenitori per le opzioni, vedere [metodi di discretizzazione &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 In alternativa, invece di usare i valori numerici, è possibile aggiungere una colonna derivata distinta che classifica i livelli di servizio in intervalli di destinazione predefiniti, ad esempio **migliore** (ServiceGrade \<= 0,05),  **Accettabili** (0,10 > ServiceGrade > 0,05), e **scarse** (ServiceGrade > = 0,10).  
  
###  <a name="bkmk_newColumn"></a> Creare una copia di una colonna e modificare il metodo di discretizzazione  
 Verrà creare una copia della colonna di data mining che contiene l'attributo di destinazione ServiceGrade e modificare il modo in cui che vengono raggruppati i numeri. Verranno quindi create più copie di qualsiasi colonna in una struttura di data mining, incluso l'attributo stimabile.  
  
 Ai fini di questa esercitazione, verrà utilizzato il metodo di discretizzazione delle aree uguali e verranno specificati quattro bucket. I raggruppamenti risultanti da questo metodo sono piuttosto vicini ai valori di destinazione di interesse per gli utenti aziendali.  
  
####  <a name="bkmk_ColumnCopy"></a> Per creare una copia personalizzata di una colonna nella struttura di data mining  
  
1.  In Esplora soluzioni fare doppio clic sulla struttura di data mining creata.  
  
2.  Nella scheda struttura di Data Mining, fare clic su **aggiungere una colonna della struttura di data mining**.  
  
3.  Nel **selezionare la colonna** selezionare ServiceGrade dall'elenco nella finestra di dialogo **colonna di origine**, quindi fare clic su **OK**.  
  
     Una nuova colonna verrà aggiunta all'elenco di colonne della struttura di data mining. Per impostazione predefinita, la nuova colonna di data mining avrà lo stesso nome della colonna esistente, seguito da un suffisso numerico, ad esempio ServiceGrade 1. È possibile modificare il nome della colonna in modo da renderlo più descrittivo.  
  
     È inoltre necessario specificare il metodo di discretizzazione.  
  
4.  Fare doppio clic su ServiceGrade 1 e selezionare **proprietà**.  
  
5.  Nel **delle proprietà** finestra, individuare il **nome** proprietà e modificare il nome in **Service Grade Binned** .  
  
6.  Verrà visualizzata una finestra di dialogo in cui viene richiesto se si desidera apportare la stessa modifica al nome di tutte le colonne del modello di data mining correlate. Fare clic su **No**.  
  
7.  Nel **delle proprietà** finestra, individuare la sezione **tipo di dati** ed espanderla, se necessario.  
  
8.  Modificare il valore della proprietà `Content` da `Continuous` in `Discretized`.  
  
     Sono ora disponibili le proprietà elencate di seguito. Modificare i valori delle proprietà come indicato nella tabella seguente:  
  
    |Proprietà|Valore predefinito|Nuovo valore|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|Nessun valore|4|  
  
    > [!NOTE]  
    >  In realtà, il valore predefinito di <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> è 0, che significa che l'algoritmo determina automaticamente il numero ottimale di bucket. Se, pertanto, si desidera reimpostare questa proprietà sul valore predefinito, digitare 0.  
  
9. Progettazione modelli di Data Mining, fare clic sui **modelli di Data Mining** scheda.  
  
     Si noti che quando si aggiunge una copia di una colonna della struttura di data mining, il flag di utilizzo per la copia viene impostato automaticamente su `Ignore`. Quando si aggiunge una copia di una colonna a una struttura di data mining, la copia non viene in genere utilizzata per l'analisi insieme alla colonna originale perché, in caso contrario, l'algoritmo individuerebbe una stretta correlazione tra le due colonne, nascondendo altre relazioni.  
  
##  <a name="bkmk_NewModel"></a> Aggiungere un nuovo modello di Data Mining alla struttura di Data Mining  
 Dopo avere creato un nuovo raggruppamento per l'attributo di destinazione, è necessario aggiungere un nuovo modello di data mining che utilizzi la colonna discretizzata. Al termine, la struttura di data mining CallCenter includerà due modelli di data mining:  
  
-   Il modello di data mining Call Center Default NN gestisce i valori di ServiceGrade come intervallo continuo.  
  
-   Si creerà un nuovo modello di data mining, Call Center Binned NN, che utilizza come risultati di destinazione i valori della colonna ServiceGrade, distribuiti in quattro bucket di uguale dimensione.  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>Per aggiungere un modello di data mining basato sulla nuova colonna discretizzata  
  
1.  In Esplora soluzioni, la struttura di data mining appena creato e scegliere **aperto**.  
  
2.  Fare clic sulla scheda **Modelli di data mining** .  
  
3.  Fare clic su **creare un modello di data mining correlato**.  
  
4.  Nel **nuovo modello di Data Mining** della finestra di dialogo per **Model name**, tipo `Call Center Binned NN`. Nel **nome dell'algoritmo** elenco a discesa, seleziona **Microsoft Neural Network**.  
  
5.  Nell'elenco di colonne contenute nel nuovo modello di data mining individuare ServiceGrade, quindi modificare l'utilizzo da `Predict` a `Ignore`.  
  
6.  Analogamente, individuare ServiceGrade Binned e modificare l'utilizzo da `Ignore` a `Predict`.  
  
##  <a name="bkmk_Alias2"></a> Creare un Alias per la colonna di destinazione  
 Non è in genere possibile confrontare modelli di data mining che utilizzano attributi stimabili diversi. È tuttavia possibile creare un alias per una colonna del modello di data mining. Vale a dire, è possibile rinominare la colonna ServiceGrade Binned all'interno del modello di data mining in modo che includa lo stesso nome della colonna originale. È quindi possibile confrontare direttamente i due modelli in un grafico di accuratezza, anche se i dati vengono discretizzati in modo diverso.  
  
###  <a name="bkmk_Alias"></a> Per aggiungere un alias per una colonna della struttura di data mining in un modello di data mining  
  
1.  Nel **modelli di Data Mining** nella scheda **struttura**, selezionare ServiceGrade Binned.  
  
     Si noti che il **proprietà** finestra vengono visualizzate le proprietà dell'oggetto, la colonna ScalarMiningStructure.  
  
2.  Nella colonna ServiceGrade Binned NN per il modello di data mining fare clic sulla cella corrispondente alla colonna ServiceGrade Binned.  
  
     Si noti che ora il **proprietà** finestra vengono visualizzate le proprietà dell'oggetto MiningModelColumn.  
  
3.  Individuare il **Name** proprietà e modificare il valore in `ServiceGrade`.  
  
4.  Individuare il **Description** proprietà e il tipo **alias di colonna temporanea**.  
  
     Il **proprietà** finestra deve contenere le informazioni seguenti:  
  
    |Proprietà|Value|  
    |--------------|-----------|  
    |**Descrizione**|Alias di colonna temporanea|  
    |**ID**|ServiceGrade Binned|  
    |**Flag di modellazione**||  
    |**Name**|Service Grade|  
    |**ID SourceColumn**|Service Grade 1|  
    |**Usage**|Stima|  
  
5.  Fare clic in qualsiasi punto nel **modello di Data Mining** scheda.  
  
     La griglia viene aggiornata per mostrare il nuovo alias di colonna temporanea, `ServiceGrade`, accanto all'utilizzo della colonna. La griglia contenente la struttura di data mining e i due modelli di data mining avranno un aspetto simile al seguente:  
  
    |Struttura|Call Center Default NN|Call Center Binned NN|  
    |---------------|----------------------------|---------------------------|  
    ||Microsoft Neural Network|Microsoft Neural Network|  
    |AutomaticResponses|Input|Input|  
    |AverageTimePerIssue|Stima|Stima|  
    |Calls|Input|Input|  
    |DayOfWeek|Input|Input|  
    |FactCallCenterID|Chiave|Chiave|  
    |IssuesRaised|Input|Input|  
    |LevelOneOperators|Input|Input|  
    |LevelTwoOperators|Input|Input|  
    |Orders|Input|Input|  
    |ServiceGrade Binned|Ignore|Predict (ServiceGrade)|  
    |ServiceGrade|Stima|Ignore|  
    |Turno|Input|Input|  
    |TotalOperators|Input|Input|  
    |WageType|Input|Input|  
  
## <a name="process-all-models"></a>Elaborare tutti i modelli  
 Per garantire che i modelli creati siano facilmente confrontabili, infine, è necessario impostare il parametro del valore di inizializzazione per entrambi i modelli. L'impostazione di un valore di inizializzazione fa sì che ciascun modello inizi a elaborare i dati dallo stesso punto.  
  
> [!NOTE]  
>  Se non si specifica un valore numerico per il parametro del valore di inizializzazione, in SQL Server Analysis Services verrà generato un valore di inizializzazione basato sul nome del modello. Poiché i modelli hanno nomi diversi, è necessario impostare un valore di inizializzazione per garantire che elaborino i dati nello stesso ordine.  
  
###  <a name="bkmk_SeedProcess"></a> Per specificare il valore di inizializzazione ed elaborare i modelli  
  
1.  Nel **modello di Data Mining** scheda, fare doppio clic su colonna per il modello denominato Call Center - LR, quindi selezionare **imposta parametri algoritmo**.  
  
2.  Nella riga del parametro HOLDOUT_SEED fare clic sulla cella vuota sotto **valore**e il tipo `1`. Fare clic su **OK**. Ripetere questo passaggio per ciascun modello associato alla struttura.  
  
    > [!NOTE]  
    >  Il valore scelto come valore di inizializzazione non è importante, a condizione che si utilizzi lo stesso valore di inizializzazione per tutti i modelli correlati.  
  
3.  Nel **modelli di Data Mining** dal menu **Elabora struttura di Data Mining e tutti i modelli**. Fare clic su **Sì** per distribuire il progetto di data mining i dati aggiornati nel server.  
  
4.  Nel **modello di processo di Data Mining** finestra di dialogo, fare clic su **eseguire**.  
  
5.  Fare clic su **chiudere** per chiudere la **stato elaborazione** la finestra di dialogo e quindi fare clic su **chiudere** nuovamente nel **Elabora modello di Data Mining** nella finestra di dialogo.  
  
 Dopo avere creato i due modelli di data mining correlati, è necessario esplorare i dati per individuarvi le relazioni.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello Call Center &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
