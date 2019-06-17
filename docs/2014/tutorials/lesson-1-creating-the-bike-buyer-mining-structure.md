---
title: 'Lezione 1: Creazione della struttura di Data Mining Bike Buyer | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a73ac60b-660f-458a-bd2f-993fbeba7226
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d6384910858d87a80aa3c8f897bc88e45f4504fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678494"
---
# <a name="lesson-1-creating-the-bike-buyer-mining-structure"></a>Lezione 1: Creazione della struttura di data mining Bike Buyer
  In questa lezione verrà creata una struttura di data mining che consente di stimare se un potenziale cliente di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] acquisterà una bicicletta. Se non si ha familiarità con le strutture di data mining e sul loro ruolo nel data mining, vedere [strutture di Data Mining &#40;Analysis Services - Data Mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md).  
  
 La struttura di data mining Bike Buyer che verrà creato in questa lezione supporta l'aggiunta di modelli di data mining in base il [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)[algoritmo Microsoft Decision Trees](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md). Nelle lezioni successive si utilizzeranno i modelli di data mining di clustering per esaminare le diverse modalità di raggruppamento dei clienti e si utilizzeranno modelli di data mining di albero delle decisioni per stimare se un potenziale cliente acquisterà una bicicletta.  
  
## <a name="create-mining-structure-statement"></a>Istruzione CREATE MINING STRUCTURE  
 Per creare una struttura di data mining, usare il [Crea struttura di data MINING &#40;DMX&#41; ](/sql/dmx/create-mining-structure-dmx) istruzione. Il codice nell'istruzione può essere suddiviso nelle parti seguenti:  
  
-   Denominazione della struttura.  
  
-   Definizione della colonna chiave.  
  
-   Definizione delle colonne di data mining.  
  
-   Definizione di un set di dati di testing facoltativo.  
  
 Di seguito è riportato un esempio generico dell'istruzione CREATE MINING STRUCTURE:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
(  
    <key column>,  
    <mining structure columns>  
)   
WITH HOLDOUT (<holdout specifier>)  
```  
  
 La prima riga del codice definisce il nome della struttura:  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
```  
  
 Per informazioni sulla denominazione di un oggetto di Data Mining Extensions (DMX), vedere [identificatori &#40;DMX&#41;](/sql/dmx/identifiers-dmx).  
  
 La riga successiva del codice definisce la colonna chiave per la struttura di data mining, che identifica in modo univoco un'entità nei dati di origine:  
  
```  
<key column>,  
```  
  
 In questa struttura di data mining creata, l'identificatore del cliente, `CustomerKey`, definisce un'entità nei dati di origine.  
  
 La riga successiva del codice è utilizzata per definire le colonne di data mining che verranno utilizzate dai modelli di data mining associati alla struttura di data mining:  
  
```  
<mining structure columns>  
```  
  
 È possibile usare la funzione DISCRETIZE in \<le colonne della struttura di data mining > per discretizzare colonne continue utilizzando la sintassi seguente:  
  
 `DISCRETIZE(<method>,<number of buckets>)`  
  
 Per altre informazioni sulla discretizzazione delle colonne, vedere [metodi di discretizzazione &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md). Per altre informazioni sui tipi di cui è possibile definire le colonne della struttura di data mining, vedere [colonne della struttura di Data Mining](../../2014/analysis-services/data-mining/mining-structure-columns.md).  
  
 L'ultima riga del codice definisce una partizione facoltativa nella struttura di data mining:  
  
```  
WITH HOLDOUT (<holdout specifier>)  
```  
  
 Specificare alcuni dati da utilizzare per testare i modelli di data mining correlati alla struttura e i rimanenti dati da utilizzare per il training dei modelli. Per impostazione predefinita, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene creato un set di dati di test che contiene il 30% di tutti i dati dei case. È necessario aggiungere la specifica che i set di dati di test devono contenere il 30% dei case fino a un massimo di 1000 case. Se il 30% dei case è minore di 1000, il set di dati di test conterrà la quantità inferiore.  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Creazione di una nuova query vuota.  
  
-   Modifica della query per creare la struttura di data mining.  
  
-   Esecuzione della query.  
  
## <a name="creating-the-query"></a>Creazione della query  
 Il primo passaggio consiste nella connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e nella creazione di una nuova query DMX in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>Per creare una nuova query DMX in SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Nel **Connetti al Server** della finestra di dialogo per **tipo di Server**, selezionare **Analysis Services**. Nelle **nome Server**, digitare `LocalHost`, oppure digitare il nome dell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che si desidera connettersi a fini di questa lezione. Fare clic su **Connetti**.  
  
3.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**e quindi fare clic su **DMX** per aprire la **Editor di Query**e una nuova query vuota.  
  
## <a name="altering-the-query"></a>Modifica della query  
 Il passaggio successivo consiste nella modifica dell'istruzione CREATE MINING STRUCTURE descritta in precedenza per creare la struttura di data mining Bike Buyer.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>Per personalizzare l'istruzione CREATE MINING STRUCTURE  
  
1.  Nell'editor di query copiare l'esempio generico dell'istruzione CREATE MINING STRUCTURE nella query vuota.  
  
2.  Sostituire quanto segue:  
  
    ```  
    [<mining structure>]   
    ```  
  
     con:  
  
    ```  
    [Bike Buyer]  
    ```  
  
3.  Sostituire quanto segue:  
  
    ```  
    <key column>   
    ```  
  
     con:  
  
    ```  
    CustomerKey LONG KEY  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    <mining structure columns>   
    ```  
  
     con:  
  
    ```  
    [Age] LONG DISCRETIZED(Automatic,10),  
    [Bike Buyer] LONG DISCRETE,  
    [Commute Distance] TEXT DISCRETE,  
    [Education] TEXT DISCRETE,  
    [Gender] TEXT DISCRETE,  
    [House Owner Flag] TEXT DISCRETE,  
    [Marital Status] TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Number Children At Home] LONG DISCRETE,  
    [Occupation] TEXT DISCRETE,  
    [Region] TEXT DISCRETE,  
    [Total Children]LONG DISCRETE,  
    [Yearly Income] DOUBLE CONTINUOUS  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    WITH HOLDOUT (holdout specifier>)  
    ```  
  
     con:  
  
    ```  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
    ```  
  
     L'istruzione della struttura di data mining completa dovrebbe essere la seguente:  
  
    ```  
    CREATE MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key] LONG KEY,  
       [Age]LONG DISCRETIZED(Automatic,10),  
       [Bike Buyer] LONG DISCRETE,  
       [Commute Distance] TEXT DISCRETE,  
       [Education] TEXT DISCRETE,  
       [Gender] TEXT DISCRETE,  
       [House Owner Flag] TEXT DISCRETE,  
       [Marital Status] TEXT DISCRETE,  
       [Number Cars Owned]LONG DISCRETE,  
       [Number Children At Home]LONG DISCRETE,  
       [Occupation] TEXT DISCRETE,  
       [Region] TEXT DISCRETE,  
       [Total Children]LONG DISCRETE,  
       [Yearly Income] DOUBLE CONTINUOUS  
    )  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
  
    ```  
  
6.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
7.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Bike Buyer Structure.dmx`.  
  
## <a name="executing-the-query"></a>Esecuzione della query  
 Il passaggio conclusivo consiste nell'esecuzione della query. Dopo la creazione e il salvataggio di una query, è necessario eseguirla. Ovvero, l'istruzione deve essere eseguita per creare la struttura di data mining nel server. Per altre informazioni sull'esecuzione di query nell'Editor di Query, vedere [Editor di Query motore di Database &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md).  
  
#### <a name="to-execute-the-query"></a>Per eseguire la query  
  
1.  Nell'Editor di Query nella barra degli strumenti, fare clic su **Execute**.  
  
     Lo stato della query viene visualizzato nei **messaggi** scheda nella parte inferiore dell'Editor di Query al termine dell'esecuzione dell'istruzione. Dovrebbero essere visualizzati i messaggi seguenti:  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     Una nuova struttura denominata **Bike Buyer** ora esista nel server.  
  
 Nella lezione successiva verranno aggiunti modelli di data mining alla struttura appena creata.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Aggiunta di modelli di Data Mining alla struttura di Data Mining Bike Buyer](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
  
  
