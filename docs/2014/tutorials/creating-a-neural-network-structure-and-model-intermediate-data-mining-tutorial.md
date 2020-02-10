---
title: Creazione di una struttura e di un modello di rete neurale (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856317"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello di rete neurale (Esercitazione intermedia sul data mining)
  Per creare un modello di data mining, è innanzitutto necessario utilizzare la Creazione guidata modello di data mining per creare una nuova struttura di data mining basata sulla nuova vista origine dati. In questa attività verrà utilizzata la procedura guidata per creare una struttura di data mining e, contemporaneamente, il modello di data mining associato basato sull'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Neural Network.  
  
 Poiché le reti neurali sono estremamente flessibili e possono analizzare molte combinazioni di input e output, è necessario sperimentare diverse modalità di elaborazione dei dati per ottenere risultati ottimali. Ad esempio, è possibile personalizzare il modo in cui la destinazione numerica per la qualità del servizio è suddivisa in *contenitori*o raggruppati per soddisfare requisiti aziendali specifici. A tale scopo, è necessario aggiungere una nuova colonna alla struttura di data mining per raggruppare i dati numerici in modi diversi, quindi creare un modello che utilizzi la nuova colonna. Questi modelli di data mining verranno utilizzati per alcune attività di esplorazione.  
  
 Dopo avere identificato, grazie al modello di rete neurale, i fattori di maggiore impatto per le questioni aziendali, sarà infine necessario compilare un modello distinto per la stima e l'assegnazione dei punteggi. Verrà utilizzato l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Logistic Regression, basato sul modello di rete neurale, ma ottimizzato per la ricerca di una soluzione basata su input specifici.  
  
 **Passaggi**  
  
 [Creare la struttura di data mining e il modello predefiniti](#bkmk_defaul)  
  
 [Utilizzare la discretizzazione per categorizzare la colonna stimabile](#bkmk_ColumnCopy)  
  
 [Copiare la colonna e modificare il metodo di discretizzazione per un altro modello](#bkmk_Alias)  
  
 [Creare un alias per la colonna stimabile in modo da poter confrontare i modelli](#bkmk_Alias2)  
  
 [Elabora tutti i modelli](#bkmk_SeedProcess)  
  
## Creare la struttura predefinita del Call Center<a name="bkmk_defaul"></a>  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse su **strutture di data mining** e scegliere **nuova struttura di data mining**  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** verificare che sia selezionato **da database relazionale o data warehouse esistente** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Crea la struttura di data mining** verificare che sia selezionata l'opzione **crea struttura di data mining con un modello di data mining** .  
  
5.  Fare clic sull'elenco a discesa dell'opzione **che data mining tecnica si desidera utilizzare**, quindi selezionare **Microsoft Neural Networks**.  
  
     Poiché i modelli di regressione logistica sono basati sulle reti neurali, è possibile riutilizzare la stessa struttura e aggiungere un nuovo modello di data mining.  
  
6.  Fare clic su **Avanti**.  
  
     Verrà visualizzata la pagina **Selezione vista origine dati** .  
  
7.  In **viste origine dati disponibili**selezionare `Call Center`, quindi fare clic su **Avanti**.  
  
8.  Nella pagina **impostazione tipi di tabelle** selezionare la casella di controllo **case** accanto alla tabella **FactCallCenter** . Non selezionare alcun valore per **DimDate**. Fare clic su **Avanti**.  
  
9. Nella pagina **impostazione dati di training** selezionare **chiave** accanto alla colonna **FactCallCenterID.**  
  
10. Selezionare le `Predict` caselle di controllo e **input** .  
  
11. Selezionare le caselle **chiave**, **input**e `Predict` casella di controllo, come illustrato nella tabella seguente:  
  
    |Tabelle/Colonne|Chiave/Input/Stima|  
    |---------------------|-------------------------|  
    |AutomaticResponses|Input|  
    |AverageTimePerIssue|Input/Stima|  
    |Calls|Input|  
    |DateKey|Non usare|  
    |DayOfWeek|Input|  
    |FactCallCenterID|Chiave|  
    |IssuesRaised|Input|  
    |LevelOneOperators|Input/Stima|  
    |LevelTwoOperators|Input|  
    |Ordini|Input/Stima|  
    |ServiceGrade|Input/Stima|  
    |MAIUSC|Input|  
    |TotalOperators|Non usare|  
    |WageType|Input|  
  
     Notare che sono state selezionate più colonne stimabili. Uno degli aspetti positivi dell'algoritmo Neural Network è la capacità di analizzare tutte le possibili combinazioni di attributi di input e output. Questa operazione non può essere eseguita per un set di dati di grandi dimensioni, perché potrebbe aumentare in modo esponenziale il tempo di elaborazione.  
  
12. Nella pagina **impostazione tipo di contenuto e dati delle colonne** verificare che la griglia contenga le colonne, i tipi di contenuto e i tipi di dati, come illustrato nella tabella seguente, quindi fare clic su **Avanti**.  
  
    |Colonne|Content Type|Tipi di dati|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|Continuo|long|  
    |AverageTimePerIssue|Continuo|long|  
    |Calls|Continuo|long|  
    |DayOfWeek|Discrete|Text|  
    |FactCallCenterID|Chiave|long|  
    |IssuesRaised|Continuo|long|  
    |LevelOneOperators|Continuo|long|  
    |LevelTwoOperators|Continuo|long|  
    |Ordini|Continuo|long|  
    |ServiceGrade|Continuo|DOUBLE|  
    |MAIUSC|Discrete|Text|  
    |WageType|Discrete|Text|  
  
13. Nella pagina **Crea set di testing** deselezionare la casella di testo per l'opzione, **percentuale di dati per il testing**. Fare clic su **Avanti**.  
  
14. Nella pagina **Completamento procedura guidata** Digitare `Call Center`per il **nome della struttura di data mining**.  
  
15. Per il **nome del modello di data mining**, digitare `Call Center Default NN`, quindi fare clic su **fine**.  
  
     La casella **Consenti drill-through** è disabilitata perché non è possibile eseguire il drill-through nei dati con i modelli di rete neurale.  
  
16. In Esplora soluzioni fare clic con il pulsante destro del mouse sul nome della struttura data mining appena creata e scegliere **elabora**.  
  
## <a name="use-discretization-to-bin-the-target-column"></a>Utilizzare la discretizzazione per categorizzare la colonna di destinazione  
 Per impostazione predefinita, quando si crea un modello di rete neurale che include un attributo stimabile numerico, tramite l'algoritmo Microsoft Neural Network l'attributo viene considerato come un numero continuo. L'attributo ServiceGrade, ad esempio, è un numero che teoricamente varia da 0,00 (risposta a tutte le chiamate) a 1,00 (tutti i chiamanti riattaccano). In questo set di dati i valori hanno la distribuzione seguente:  
  
 ![Distribuzione dei valori del livello di servizio](../../2014/tutorials/media/skt-service-grade-valuesc.gif "Distribuzione dei valori del livello di servizio")  
  
 Di conseguenza, quando si elabora il modello, gli output possono essere raggruppati in modo diverso dal previsto. Se ad esempio si usa il clustering per identificare i gruppi di valori migliori, l'algoritmo divide i valori in ServiceGrade in intervalli come il seguente: 0,0748051948-0,09716216215. Benché questo raggruppamento sia matematicamente preciso, gli intervalli potrebbero non essere altrettanto significativi per gli utenti aziendali.  
  
 In questo passaggio, per rendere più intuitivo il risultato, è necessario raggruppare i valori numerici in modo diverso, creando copie della colonna di dati numerici.  
  
### <a name="how-discretization-works"></a>Funzionamento della discretizzazione  
 Analysis Services offre un'ampia gamma di metodi per suddividere in contenitori o elaborare dati numerici. Nella tabella seguente vengono illustrate le differenze tra i risultati quando l'attributo di output ServiceGrade viene elaborato in tre modi diversi, ovvero:  
  
-   Considerandolo un numero continuo.  
  
-   Lasciando che l'algoritmo utilizzi il clustering per identificare la migliore disposizione di valori.  
  
-   Specificando che i numeri siano inseriti in contenitori in base al metodo delle aree uguali,  
  
 Modello predefinito (continuo)  
  
|VALORE|SUPPORTO|  
|-----------|-------------|  
|Missing|0|  
|0,09875|120|  
  
 Suddiviso tramite clustering  
  
|VALORE|SUPPORTO|  
|-----------|-------------|  
|\<0,0748051948|34|  
|0,0748051948-0,09716216215|27|  
|0,09716216215-0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 Suddiviso in base al metodo delle aree uguali  
  
|VALORE|SUPPORTO|  
|-----------|-------------|  
|\<0,07|26|  
|0,07-0,00|22|  
|0,09-0,11|36|  
|>= 0,12|36|  
  
> [!NOTE]  
>  È possibile ottenere tali statistiche dal nodo delle statistiche marginali del modello al termine dell'elaborazione di tutti i dati. Per ulteriori informazioni sul nodo delle statistiche marginali, vedere il [contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services-&#41;di data mining ](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 Nella colonna VALUE di questa tabella è indicato come è stato gestito il numero per ServiceGrade. Nella colonna SUPPORT è indicato quanti case avevano tale valore o rientravano in tale intervallo.  
  
-   **Utilizzare numeri continui (valore predefinito)**  
  
     Se è stato utilizzato il metodo predefinito, l'algoritmo calcolerà i risultati per 120 valori distinti, il cui valore medio è 0,09875. È inoltre possibile visualizzare il numero di valori mancanti.  
  
-   **Suddividere tramite clustering**  
  
     Quando si consente all'algoritmo Microsoft Clustering di determinare il raggruppamento facoltativo dei valori, i valori per ServiceGrade verranno raggruppati in cinque (5) intervalli. Il numero di case in ogni intervallo non viene distribuito uniformemente, come si vedere nella colonna Support.  
  
-   **Suddividere in base al metodo delle aree uguali**  
  
     Quando si sceglie questo metodo, l'algoritmo forza i valori in bucket di uguale dimensione che a loro volta modificano i limiti superiori e inferiori di ogni intervallo. È possibile specificare il numero di bucket, ma è consigliabile evitare di avere bucket contenenti solo pochi valori.  
  
 Per ulteriori informazioni sulle opzioni di suddivisione in contenitori, vedere [metodi di discretizzazione &#40;&#41;di data mining ](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 In alternativa, anziché usare i valori numerici, è possibile aggiungere una colonna derivata distinta che classifica i livelli di servizio in intervalli di destinazione predefiniti, ad esempio **Best** (ServiceGrade \<= 0,05), **accettabile** (0,10 > ServiceGrade > 0,05) e **poor** (ServiceGrade >= 0,10).  
  
###  <a name="bkmk_newColumn"></a>Creare una copia di una colonna e modificare il metodo di discretizzazione  
 Verrà fatta una copia della colonna di data mining che contiene l'attributo di destinazione, ServiceGrade, e verrà modificata la modalità di raggruppamento dei numeri. Verranno quindi create più copie di qualsiasi colonna in una struttura di data mining, incluso l'attributo stimabile.  
  
 Ai fini di questa esercitazione, verrà utilizzato il metodo di discretizzazione delle aree uguali e verranno specificati quattro bucket. I raggruppamenti risultanti da questo metodo sono piuttosto vicini ai valori di destinazione di interesse per gli utenti aziendali.  
  
####  <a name="bkmk_ColumnCopy"></a>Per creare una copia personalizzata di una colonna nella struttura di data mining  
  
1.  In Esplora soluzioni fare doppio clic sulla struttura di data mining creata.  
  
2.  Nella scheda struttura di data mining fare clic su **Aggiungi una colonna della struttura di data mining**.  
  
3.  Nella finestra di dialogo **Seleziona colonna** selezionare ServiceGrade dall'elenco in colonna di **origine**, quindi fare clic su **OK**.  
  
     Una nuova colonna verrà aggiunta all'elenco di colonne della struttura di data mining. Per impostazione predefinita, la nuova colonna di data mining avrà lo stesso nome della colonna esistente, seguito da un suffisso numerico, ad esempio ServiceGrade 1. È possibile modificare il nome della colonna in modo da renderlo più descrittivo.  
  
     È inoltre necessario specificare il metodo di discretizzazione.  
  
4.  Fare clic con il pulsante destro del mouse su ServiceGrade 1 e scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** individuare la proprietà **Name** e modificare il nome in **servizio di livello di servizio** .  
  
6.  Verrà visualizzata una finestra di dialogo in cui viene richiesto se si desidera apportare la stessa modifica al nome di tutte le colonne del modello di data mining correlate. Fare clic su **No**.  
  
7.  Nella finestra **Proprietà** individuare il **tipo di dati** della sezione ed espanderlo, se necessario.  
  
8.  Modificare il valore della proprietà `Content` da `Continuous` in `Discretized`.  
  
     Sono ora disponibili le proprietà elencate di seguito. Modificare i valori delle proprietà come indicato nella tabella seguente:  
  
    |Proprietà|Valore predefinito|Nuovo valore|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|Nessun valore|4|  
  
    > [!NOTE]  
    >  In realtà, il valore predefinito di <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> è 0, che significa che l'algoritmo determina automaticamente il numero ottimale di bucket. Se, pertanto, si desidera reimpostare questa proprietà sul valore predefinito, digitare 0.  
  
9. In Progettazione modelli di data mining fare clic sulla scheda **modelli di data mining** .  
  
     Si noti che quando si aggiunge una copia di una colonna della struttura di data mining, il flag di utilizzo per la copia viene impostato automaticamente su `Ignore`. Quando si aggiunge una copia di una colonna a una struttura di data mining, la copia non viene in genere utilizzata per l'analisi insieme alla colonna originale perché, in caso contrario, l'algoritmo individuerebbe una stretta correlazione tra le due colonne, nascondendo altre relazioni.  
  
##  <a name="bkmk_NewModel"></a>Aggiungere un nuovo modello di data mining alla struttura di data mining  
 Dopo avere creato un nuovo raggruppamento per l'attributo di destinazione, è necessario aggiungere un nuovo modello di data mining che utilizzi la colonna discretizzata. Al termine, la struttura di data mining CallCenter includerà due modelli di data mining:  
  
-   Il modello di data mining Call Center Default NN gestisce i valori di ServiceGrade come intervallo continuo.  
  
-   Verrà creato un nuovo modello di data mining, Call Center con contenitori NN, che utilizza come risultati di destinazione i valori della colonna ServiceGrade, distribuiti in quattro bucket di uguale dimensione.  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>Per aggiungere un modello di data mining basato sulla nuova colonna discretizzata  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sulla struttura di data mining appena creata e scegliere **Apri**.  
  
2.  Fare clic sulla scheda **Modelli di data mining** .  
  
3.  Fare clic su **Crea un modello di data mining correlato**.  
  
4.  Nella finestra di dialogo **nuovo modello di data mining** Digitare `Call Center Binned NN`per **nome modello**. Nell'elenco a discesa **Nome algoritmo** selezionare **Microsoft Neural Network**.  
  
5.  Nell'elenco di colonne contenute nel nuovo modello di data mining individuare ServiceGrade, quindi modificare l'utilizzo da `Predict` a `Ignore`.  
  
6.  Analogamente, individuare ServiceGrade Binned e modificare l'utilizzo da `Ignore` a `Predict`.  
  
##  <a name="bkmk_Alias2"></a>Creare un alias per la colonna di destinazione  
 Non è in genere possibile confrontare modelli di data mining che utilizzano attributi stimabili diversi. È tuttavia possibile creare un alias per una colonna del modello di data mining. Ovvero, è possibile rinominare la colonna ServiceGrade in contenitori, all'interno del modello di data mining in modo che abbia lo stesso nome della colonna originale. È quindi possibile confrontare direttamente i due modelli in un grafico di accuratezza, anche se i dati vengono discretizzati in modo diverso.  
  
###  <a name="bkmk_Alias"></a>Per aggiungere un alias per una colonna della struttura di data mining in un modello di data mining  
  
1.  Nella scheda **modelli di data mining** , in **struttura**, selezionare ServiceGrade contenitori.  
  
     Si noti che nella finestra **Proprietà** vengono visualizzate le proprietà dell'oggetto, ScalarMiningStructure colonna.  
  
2.  Nella colonna ServiceGrade Binned NN per il modello di data mining fare clic sulla cella corrispondente alla colonna ServiceGrade Binned.  
  
     Si noti che ora nella finestra **Proprietà** vengono visualizzate le proprietà per l'oggetto, MiningModelColumn.  
  
3.  Individuare la proprietà **Name** e modificare il valore in `ServiceGrade`.  
  
4.  Individuare la proprietà **Description** e digitare **alias di colonna temporanea**.  
  
     La finestra **Proprietà** deve contenere le seguenti informazioni:  
  
    |Proprietà|valore|  
    |--------------|-----------|  
    |**Descrizione**|Alias di colonna temporanea|  
    |**ID**|ServiceGrade Binned|  
    |**Flag di modellazione**||  
    |**Nome**|Service Grade|  
    |**SourceColumn ID**|Service Grade 1|  
    |**Utilizzo**|Stima|  
  
5.  Fare clic in un punto qualsiasi della scheda **modello di data mining** .  
  
     La griglia viene aggiornata per mostrare il nuovo alias di colonna temporanea `ServiceGrade`,, accanto all'utilizzo della colonna. La griglia contenente la struttura di data mining e i due modelli di data mining avranno un aspetto simile al seguente:  
  
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
    |Ordini|Input|Input|  
    |ServiceGrade Binned|Ignora|Predict (ServiceGrade)|  
    |ServiceGrade|Stima|Ignora|  
    |MAIUSC|Input|Input|  
    |TotalOperators|Input|Input|  
    |WageType|Input|Input|  
  
## <a name="process-all-models"></a>Elaborare tutti i modelli  
 Per garantire che i modelli creati siano facilmente confrontabili, infine, è necessario impostare il parametro del valore di inizializzazione per entrambi i modelli. L'impostazione di un valore di inizializzazione fa sì che ciascun modello inizi a elaborare i dati dallo stesso punto.  
  
> [!NOTE]  
>  Se non si specifica un valore numerico per il parametro del valore di inizializzazione, in SQL Server Analysis Services verrà generato un valore di inizializzazione basato sul nome del modello. Poiché i modelli hanno nomi diversi, è necessario impostare un valore di inizializzazione per garantire che elaborino i dati nello stesso ordine.  
  
###  <a name="bkmk_SeedProcess"></a>Per specificare il valore di inizializzazione ed elaborare i modelli  
  
1.  Nella scheda **modello di data mining** fare clic con il pulsante destro del mouse sulla colonna per il modello denominato Call Center-LR, quindi scegliere **Imposta parametri algoritmo**.  
  
2.  Nella riga relativa al parametro HOLDOUT_SEED fare clic sulla cella vuota in **valore**, quindi digitare `1`. Fare clic su **OK**. Ripetere questo passaggio per ciascun modello associato alla struttura.  
  
    > [!NOTE]  
    >  Il valore scelto come valore di inizializzazione non è importante, a condizione che si utilizzi lo stesso valore di inizializzazione per tutti i modelli correlati.  
  
3.  Scegliere **Elabora struttura di data mining e tutti i modelli**dal menu **modelli di data mining** . Fare clic su **Sì** per distribuire il progetto data mining aggiornato al server.  
  
4.  Nella finestra di dialogo **Elabora modello di data mining** fare clic su **Esegui**.  
  
5.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Stato elaborazione** , quindi fare di nuovo clic su **Chiudi** nella finestra di dialogo **Elabora modello di data mining** .  
  
 Dopo avere creato i due modelli di data mining correlati, è necessario esplorare i dati per individuarvi le relazioni.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esplorazione del modello di Call Center &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
