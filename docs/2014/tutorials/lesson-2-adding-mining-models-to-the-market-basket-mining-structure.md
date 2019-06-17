---
title: 'Lezione 2: Aggiunta di modelli di Data Mining alla struttura di Data Mining Market Basket | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204717"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>Lezione 2: Aggiunta di modelli di data mining alla struttura di data mining Market Basket
  In questa lezione verranno aggiunti due modelli di data mining alla struttura di data mining Market Basket creata in [lezione 1: Creazione della struttura di Data Mining Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md). Questi modelli di data mining consentiranno di creare stime.  
  
 Per stimare quali tipi di prodotti i clienti tendono ad acquistare contemporaneamente, si creerà due modelli di data mining utilizzando il [algoritmo Microsoft Association Rules](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md) e due valori diversi per il *MINIMUM_PROBABILTY* parametro.  
  
 *MINIMUM_PROBABILTY* è un [!INCLUDE[msCoName](../includes/msconame-md.md)] parametro algoritmo Association che aiuta a determinare il numero di regole che un modello di data mining conterrà specificando la probabilità minima che deve avere una regola. Ad esempio, l'impostazione di questo valore su 0,4 specifica che una regola può essere generata solo se la combinazione di prodotti che la regola descrive ha una probabilità di realizzazione di almeno il 40%.  
  
 Si visualizzeranno l'effetto della modifica il *MINIMUM_PROBABILTY* parametro in una lezione successiva.  
  
## <a name="alter-mining-structure-statement"></a>Istruzione ALTER MINING STRUCTURE  
 Per aggiungere un modello di data mining che contiene una tabella nidificata a una struttura di data mining, si utilizza il [ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016) istruzione. Il codice nell'istruzione può essere suddiviso nelle parti seguenti:  
  
-   Identificazione della struttura di data mining  
  
-   Denominazione del modello di data mining  
  
-   Definizione della colonna chiave  
  
-   Definizione della colonna di input e della colonna stimabile  
  
-   Definizione delle colonne della tabella nidificata  
  
-   Identificazione delle modifiche a livello di algoritmo e parametri  
  
 Gli elementi seguenti sono un esempio generico dell'istruzione `ALTER MINING STRUCTURE`, che consente di aggiungere un modello di data mining a una struttura che include colonne delle tabelle nidificate:  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 La prima riga del codice identifica la struttura di data mining esistente a cui verrà aggiunto il modello di data mining:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 La riga successiva del codice indica il nome del modello di data mining che verrà aggiunto alla struttura di data mining:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Per informazioni sulla denominazione di un oggetto di Data Mining Extensions (DMX), vedere [identificatori &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 Le successive righe del codice definiscono le colonne della struttura di data mining che verranno utilizzate dal modello di data mining:  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 È possibile utilizzare solo colonne che esistono già nella struttura di data mining.  
  
 La prima colonna nell'elenco delle colonne del modello di data mining deve essere la colonna chiave nella struttura di data mining. Tuttavia, non è necessario digitare `KEY` dopo la colonna chiave per specificare l'utilizzo. Ciò avviene perché la colonna è già stata definita come colonna chiave al momento della creazione della struttura di data mining.  
  
 Le righe rimanenti specificano l'utilizzo delle colonne nel nuovo modello di data mining. Per specificare che una colonna nel modello di data mining verrà utilizzata per la stima, è possibile utilizzare la sintassi seguente:  
  
```  
<column name> PREDICT,  
```  
  
 Se non viene specificato l'utilizzo, non è necessario includere una colonna della struttura di data mining nell'elenco. Tutte le colonne utilizzate dalla struttura di data mining di riferimento sono automaticamente disponibili per l'utilizzo da parte dei modelli di data mining basati su tale struttura. Tuttavia, il modello non utilizzerà le colonne per il training a meno che non venga specificato l'utilizzo.  
  
 L'ultima riga del codice definisce l'algoritmo e i parametri dell'algoritmo che verranno utilizzati per generare il modello di data mining.  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Aggiunta di un modello di data mining di associazione alla struttura utilizzando il valore di probabilità predefinito  
  
-   Aggiunta di un modello di data mining di associazione alla struttura utilizzando un valore di probabilità modificato  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>Aggiunta di un modello di data mining di associazione alla struttura utilizzando il valore predefinito di MINIMUM_PROBABILITY  
 La prima attività consiste nell'aggiungere un nuovo modello di data mining alla struttura di data mining Market Basket in base il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo di associazione utilizzando il valore predefinito per *MINIMUM_PROBABILITY*.  
  
#### <a name="to-add-an-association-mining-model"></a>Per aggiungere un modello di data mining di associazione  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
    > [!NOTE]  
    >  Per creare una query DMX su un database [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specifico, fare clic con il pulsante destro del mouse sul database anziché sull'istanza.  
  
2.  Copiare l'esempio generico dell'istruzione `ALTER MINING STRUCTURE` nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <mining structure name>   
    ```  
  
     con:  
  
    ```  
    [Market Basket]  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining model name>   
    ```  
  
     con:  
  
    ```  
    [Default Association]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     con:  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     In questo caso, la tabella `[Products]` è stata definita come colonna stimabile`.` Inoltre, la colonna `[Model]` è inclusa nell'elenco delle colonne della tabella nidificata, poiché è la colonna chiave della tabella nidificata.  
  
    > [!NOTE]  
    >  Tenere presente che una chiave nidificata è diversa da una chiave del case. Una chiave del case è un identificatore univoco del case, mentre la chiave nidificata è un attributo che si desidera modellare.  
  
6.  Sostituire quanto segue:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     con:  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     L'istruzione risultante dovrebbe essere la seguente:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
8.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Default_Association_Model.dmx`.  
  
9. Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>Aggiunta di un modello di data mining di associazione alla struttura modificando il valore predefinito di MINIMUM_PROBABILITY  
 L'attività successiva consiste nell'aggiunta di un nuovo modello di data mining alla struttura di data mining Market Basket in base all'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association modificando il valore predefinito di MINIMUM_PROBABILITY in 0,01. La modifica del parametro determinerà la creazione di ulteriori regole da parte dell'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Association.  
  
#### <a name="to-add-an-association-mining-model"></a>Per aggiungere un modello di data mining di associazione  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione `ALTER MINING STRUCTURE` nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <mining structure name>   
    ```  
  
     con:  
  
    ```  
    Market Basket  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining model name>   
    ```  
  
     con:  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     con:  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     In questo caso, la tabella `[Products]` è stata designata come colonna stimabile. Anche la colonna `[MODEL]` è inclusa nell'elenco perché è la colonna chiave nella tabella nidificata.  
  
6.  Sostituire quanto segue:  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     con:  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     L'istruzione risultante dovrebbe essere la seguente:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
8.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Modified Association_Model.dmx`.  
  
9. Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
 Nella lezione successiva verranno elaborati la struttura di data mining Market Basket insieme ai relativi modelli di data mining associati.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: L'elaborazione della struttura di Data Mining Market Basket](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
