---
title: Applicare funzioni di stima a un modello | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
author: minewiskan
ms.author: owend
ms.openlocfilehash: fde9de00adaa1712a9db6e18aabc6a83dd660efb
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525319"
---
# <a name="apply-prediction-functions-to-a-model"></a>Applicare le funzioni di stima a un modello
  Per creare una query di stima, è innanzitutto necessario selezionare il modello di data mining su cui basare la query. È possibile selezionare qualsiasi modello di data mining esistente nel progetto corrente.  
  
 Dopo avere selezionato un modello, aggiungere una *funzione di stima* alla query. Si tratta di un'importazione per comprendere che le funzioni di stima vengono utilizzate per molti scopi: Sì, è possibile stimare i valori, ma è anche possibile ottenere le statistiche correlate, nonché le informazioni utilizzate per generare la stima. Le funzioni di stima possono restituire i tipi seguenti di valori:  
  
-   Nome dell'attributo di stima e valore che viene stimato.  
  
-   Statistiche sulla distribuzione e varianza dei valori stimati.  
  
-   Probabilità di un risultato specificato o di tutti i possibili risultati.  
  
-   Punteggi superiori o inferiori o valori.  
  
-   Valori associati a un nodo, un oggetto o un attributo specificato.  
  
 È disponibile un'ampia varietà di funzioni di stima che è possibile utilizzare, tuttavia è necessario scegliere la funzione che indica il tipo di modello creato. In genere questa scelta dipende dall'algoritmo utilizzato per creare il modello.  
  
-   Per un elenco delle funzioni di stima supportate per quasi tutti i tipi di modello, vedere [Funzioni di stima generali &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
-   I singoli algoritmi supportano inoltre una varietà di funzioni specializzate. Ad esempio, se si crea un modello di data mining basato sull'algoritmo Microsoft Clustering, è possibile utilizzare funzioni di stima specializzate per trovare informazioni sui cluster, ad esempio la distanza da un valore di dati al centro del cluster.  
  
     Per alcuni esempi di come eseguire una query su un tipo specifico di modello di data mining, vedere l'argomento di riferimento sugli algoritmi in [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>Scegliere un modello di data mining da utilizzare per la stima  
  
1.  Da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul modello e scegliere **Compila query di stima**.  
  
     -oppure-  
  
     In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sulla scheda **Stima modello di data mining**e quindi scegliere **Seleziona modello** nella tabella  **Modello di data mining** .  
  
2.  Nella finestra di dialogo **Seleziona modello di data mining** selezionare un modello di data mining e quindi fare clic su **OK**.  
  
     È possibile scegliere qualsiasi modello all'interno del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] corrente. Per creare una query utilizzando un modello in un database diverso, è necessario aprire una nuova finestra Query nel contesto di quel database oppure aprire il file della soluzione che contiene tale modello.  
  
### <a name="add-prediction-functions-to-a-query"></a>Aggiungere funzioni di stima a una query  
  
1.  In **Generatore delle query di stima**configurare i dati di input usati per la stima, specificando i valori nella finestra di dialogo **Input query singleton** o eseguendo il mapping del modello a un'origine dati esterna.  
  
     Per altre informazioni, vedere [Scegliere ed eseguire il mapping di dati di input per una query di stima](choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  Non è necessario fornire input per generare stime. In assenza di input, l'algoritmo restituisce in genere il valore stimato più probabile attraverso tutti i possibili input.  
  
2.  Fare clic sulla colonna **Origine** e scegliere un valore nell'elenco:  
  
    |||  
    |-|-|  
    |**\<model name>**|Selezionare questa opzione per includere i valori del modello di data mining nell'output. È possibile aggiungere unicamente colonne stimabili.<br /><br /> Quando si aggiunge una colonna dal modello, il risultato restituito è l'elenco non distinto di valori in quella colonna.<br /><br /> Le colonne che si aggiungono tramite questa opzione sono incluse nella parte SELECT dell'istruzione DMX risultante.|  
    |**Prediction Function**|Selezionare questa opzione per esplorare un elenco di funzioni di stima.<br /><br /> I valori o le funzioni selezionate vengono aggiunte alla parte SELECT dell'istruzione DMX risultante.<br /><br /> L'elenco di funzioni di stima non è filtrato o vincolato dal tipo di modello selezionato. Pertanto, se non si sa con sicurezza se la funzione è supportata per il tipo di modello corrente, è possibile aggiungerla all'elenco e assicurarsi che non si verifichi alcun errore.<br /><br /> Gli elementi dell'elenco preceduti da $ (AdjustedProbability $) rappresentano le colonne della tabella nidificata che viene restituita quando si utilizza la funzione, `PredictHistogram`. Si tratta di collegamenti che è possibile utilizzare per restituire una singola colonna e non una tabella nidificata.|  
    |**Espressione personalizzata**|Selezionare questa opzione per digitare un'espressione personalizzata e quindi assegnare un alias all'output.<br /><br /> L'espressione personalizzata viene aggiunta alla parte SELECT della query di stima DMX risultante.<br /><br /> Questa opzione è utile se si desidera aggiungere del testo per l'output con ogni riga, per chiamare funzioni VB o stored procedure personalizzate.<br /><br /> Per informazioni sull'uso di funzioni VBA e di Excel da DMX, vedere [Funzioni VBA in MDX e DAX](/sql/mdx/vba-functions-in-mdx-and-dax).|  
  
3.  Dopo avere aggiunto ogni funzione o espressione, passare alla vista DMX per vedere come la funzione viene aggiunta all'interno dell'istruzione DMX.  
  
    > [!WARNING]  
    >  Il Generatore delle query di stima non convalida l'istruzione DMX finché non si fa clic su **Risultati**. Spesso, l'espressione che viene prodotta dal generatore di query non è una DMX valida. Le cause tipiche sono una colonna che non è correlata alla colonna stimabile o il tentativo di stimare una colonna in una tabella nidificata che richiede un'istruzione sub-SELECT. A questo punto, è possibile passare a vista DMX e continuare a modificare l'istruzione.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>Esempio: creare una query in un modello di clustering  
  
1.  Se non è disponibile un modello di clustering per la generazione di questa query di esempio, creare il modello [TM_Clustering] facendo riferimento a [Esercitazione di base sul data mining](../../tutorials/basic-data-mining-tutorial.md).  
  
2.  Da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse sul modello [TM_Clustering] e scegliere **Compila query di stima**.  
  
3.  Scegliere **Query singleton** dal menu **Modello di data mining**.  
  
4.  Nella finestra di dialogo **Input query singleton** impostare i valori seguenti come input:  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  Nella griglia della query per **Origine**selezionare il modello di data mining TM_Clustering e aggiungere la colonna [Bike Buyer].  
  
6.  Per **origine**, selezionare **funzione di stima**e aggiungere la funzione, `Cluster` .  
  
7.  Per **origine**selezionare **funzione di stima**, aggiungere la funzione, `PredictSupport` e trascinare la colonna del modello [Bike Buyer] nella casella **criteri/argomento** . Digitare **Supporto** nella colonna **Alias** .  
  
     Copiare l'espressione che rappresenta la funzione di stima e il riferimento alla colonna dalla casella **Criteri/Argomento** .  
  
8.  Per **Origine**selezionare **Espressione personalizzata**, digitare un alias e quindi fare riferimento alla funzione CEILING di Excel usando la sintassi seguente:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Incollare il riferimento alla colonna come argomento alla funzione.  
  
     Ad esempio, l'espressione seguente restituisce il valore CEILING del valore di supporto:  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     Digitare CEILING nella colonna **Alias** .  
  
9. Fare clic su **Passa alla visualizzazione del testo della query** per esaminare l'istruzione DMX generata e quindi fare clic su **Passa alla visualizzazione dei risultati della query** per visualizzare l'output delle colonne restituito dalla query di stima.  
  
     Nella tabella seguente vengono illustrati i risultati previsti:  
  
    |Bike Buyer|$Cluster|SUPPORT|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Cluster 8|954|953.948638926372|  
  
 Se si desidera aggiungere altre clausole altrove nell'istruzione, ad esempio se si desidera aggiungere una clausola WHERE, non è possibile aggiungerla utilizzando la griglia; per prima cosa, è necessario passare alla visualizzazione DMX.  
  
## <a name="see-also"></a>Vedere anche  
 [Query di data mining](data-mining-queries.md)  
  
  
