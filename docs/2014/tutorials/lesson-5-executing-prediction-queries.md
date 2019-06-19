---
title: "Lezione 5: L'esecuzione di query di stima | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822313"
---
# <a name="lesson-5-executing-prediction-queries"></a>Lezione 5: Esecuzione di query di stima
  In questa lezione si userà il [SELECT FROM \<model > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) forma dell'istruzione SELECT per creare due tipi diversi di stime basate su albero delle decisioni del modello creato in [ Lezione 2: Aggiunta di modelli di Data Mining alla struttura di Data Mining di associazione](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md). Di seguito è riportata la definizione di questi tipi di stima.  
  
 Query singleton  
 Utilizzare una query singleton per fornire valori ad hoc in caso di esecuzione di stime. È ad esempio possibile determinare se un cliente sia il probabile acquirente di una bicicletta passando alla query input come la distanza dal luogo di lavoro, il prefisso telefonico o il numero di figli del cliente. La query singleton restituisce un valore che indica con quale probabilità il cliente acquisterà una bicicletta in base agli input forniti.  
  
 Query batch  
 Una query batch consente di determinare quali clienti, all'interno di una tabella di potenziali clienti, è probabile che acquistino una bicicletta. Ad esempio, se il reparto marketing fornisce un elenco di clienti con i relativi attributi, è possibile utilizzare una stima batch per stabilire quali di essi è probabile che acquistino una bicicletta.  
  
 Il [SELECT FROM \<model > PREDICTION JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx) forma dell'istruzione SELECT contiene tre parti:  
  
-   Un elenco di funzioni di stima e di colonne del modello di data mining restituite nei risultati. I risultati possono anche includere le colonne di input provenienti dall'origine dati.  
  
-   La query di origine che definisce i dati utilizzati per la creazione di una stima, ad esempio un elenco di clienti in una query batch.  
  
-   Un mapping tra le colonne del modello di data mining e i dati di origine. Se i nomi corrispondono, è possibile utilizzare la sintassi NATURAL e tralasciare i mapping delle colonne.  
  
 Per migliorare ulteriormente la query, è possibile utilizzare le funzioni di stima che forniscono informazioni aggiuntive, quali la probabilità che una stima sia confermata dai fatti, e supporto per la stima nel set di dati di training. Per altre informazioni sulle funzioni di stima, vedere [funzioni &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
 Le stime in questa esercitazione sono basate sulla tabella ProspectiveBuyer nel database di esempio [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. La tabella ProspectiveBuyer contiene un elenco di potenziali clienti con le relative caratteristiche. I clienti in questa tabella sono indipendenti dai clienti utilizzati per creare il modello di data mining dell'albero delle decisioni.  
  
 È inoltre possibile creare stime utilizzando il generatore delle query di stima in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Creazione di una query singleton per determinare la probabilità che un particolare cliente acquisti una bicicletta.  
  
-   Creazione di una query batch per determinare quali clienti, all'interno di una tabella di clienti, è probabile che acquistino una bicicletta.  
  
## <a name="singleton-query"></a>Query singleton  
 Il primo passaggio consiste nell'usare la [SELECT FROM &#60;modello&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) in una query di stima singleton. Di seguito è riportato un esempio generico dell'istruzione singleton:  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 La prima riga del codice definisce le colonne del modello di data mining restituite dalla query e specifica il modello di data mining utilizzato per generare la stima:  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 Le successive righe del codice definiscono le caratteristiche del cliente utilizzate per creare una stima:  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 Se si specifica NATURAL PREDICTION JOIN, il server ricercherà la corrispondenza tra ogni colonna del modello e una colonna dell'input, in base ai nomi delle colonne. Se i nomi di colonna non corrispondono, le colonne vengono ignorate.  
  
#### <a name="to-create-a-singleton-prediction-query"></a>Per creare una query di stima singleton  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione singleton nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     L'istruzione AS viene utilizzata per creare un alias delle colonne restituite dalla query. Il [PredictHistogram](/sql/dmx/predicthistogram-dmx) funzione restituisce le statistiche sulla stima, compresa la probabilità e supporto. Per altre informazioni sulle funzioni che possono essere utilizzati in un'istruzione di stima, vedere [funzioni &#40;DMX&#41;](/sql/dmx/functions-dmx).  
  
4.  Sostituire quanto segue:  
  
    ```  
    [<mining model>]   
    ```  
  
     con:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Sostituire quanto segue:  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     con:  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
7.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Singleton_Query.dmx`.  
  
8.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituisce una stima sulla probabilità che un cliente con le caratteristiche specificate acquisti una bicicletta, nonché le statistiche relative a tale stima.  
  
## <a name="batch-query"></a>Query batch  
 Il passaggio successivo consiste nell'usare la [SELECT FROM &#60;modello&#62; PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx) in una query di stima batch. Di seguito è riportato un esempio generico di istruzione batch:  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 Come nella query singleton, le prime due righe del codice definiscono le colonne del modello di data mining restituite dalla query, nonché il nome del modello di data mining utilizzato per generare la stima. La parte superiore \<numero > istruzione specifica che la query restituirà solo il numero o i risultati specificati da \<numero >.  
  
 Le successive righe del codice definiscono i dati di origine su cui si basano le stime:  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 Sebbene siano disponibili diverse opzioni per il recupero dei dati di origine, in questa esercitazione si utilizzerà OPENQUERY. Per altre informazioni sulle opzioni disponibili, vedere [ &#60;query sull'origine dati&#62;](/sql/dmx/source-data-query).  
  
 La riga successiva definisce il mapping tra le colonne di origine nel modello di data mining e le colonne nei dati di origine:  
  
```  
ON <column mappings>  
```  
  
 La clausola WHERE filtra i risultati restituiti dalla query di stima:  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 L'ultima riga (facoltativa) del codice specifica la colonna in base alla quale verranno ordinati i risultati:  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 Utilizzare ORDER BY in combinazione con il primo \<numero > istruzione, per filtrare i risultati restituiti. In questa stima, ad esempio, verranno restituiti i primi dieci acquirenti di biciclette, ordinati in base alla probabilità che la stima si riveli corretta. È possibile utilizzare la sintassi [DESC|ASC] per controllare l'ordine di visualizzazione dei risultati.  
  
#### <a name="to-create-a-batch-prediction-query"></a>Per creare una query di stima batch  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico di istruzione batch nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     La clausola TOP 10 specifica che la query restituirà solo i primi dieci risultati. L'istruzione ORDER BY nella query consente di ordinare i risultati in base alla probabilità che la stima si riveli corretta. Verranno quindi restituiti solo i dieci risultati con un grado di probabilità maggiore.  
  
4.  Sostituire il segnaposto seguente:  
  
    ```  
    [<mining model>]   
    ```  
  
     Con il nome del modello:  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  Sostituire l'istruzione generica OPENQUERY seguente:  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     Con un'istruzione che faccia riferimento al data warehouse Adventureworks corrente, ad esempio:  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  Sostituire la sintassi generica seguente:  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     Con i mapping delle colonne necessari per questo modello e per il set di dati di input:  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     Specificare `DESC` per fare in modo che l'elenco dei risultati inizi dalla probabilità più alta.  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
8.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `Batch_Prediction.dmx`.  
  
9. Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituisce una tabella con i nomi dei clienti, una stima relativa all'acquisto di una bicicletta da parte di ogni cliente e la probabilità che la stima si riveli corretta.  
  
 Si conclude così l'esercitazione Bike Buyer. A questo punto si dispone di un set di modelli di data mining che è possibile utilizzare per valutare le analogie tra i propri clienti e stimare se i potenziali clienti acquisteranno una bicicletta.  
  
 Per informazioni su come usare DMX in uno scenario Market Basket, vedere [esercitazione su DMX per Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md).  
  
  
