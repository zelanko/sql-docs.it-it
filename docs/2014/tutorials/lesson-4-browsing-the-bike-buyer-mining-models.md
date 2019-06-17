---
title: 'Lezione 4: Esplorazione di modelli di Data Mining Bike Buyer | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63070891"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>Lezione 4: Esplorazione dei modelli di data mining Bike Buyer
  In questa lezione si userà il [SELECT (DMX)](/sql/dmx/select-dmx) istruzione per esplorare il contenuto dell'albero delle decisioni e di data mining di clustering di modelli creati nella [lezione 2: Aggiunta di modelli di Data Mining alla struttura di Data Mining predittiva](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Le colonne contenute in un modello di data mining non sono quelle definite dalla struttura di data mining ma sono un set specifico di colonne che descrivono le tendenze e gli schemi individuati dall'algoritmo. Queste colonne del modello di data mining sono descritte nel [set di righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset) set di righe dello schema. La colonna MODEL_NAME nel set di righe dello schema del contenuto, ad esempio, contiene il nome del modello di data mining. Per un modello di data mining di clustering, la colonna NODE_CAPTION contiene il nome di ogni cluster e la colonna NODE_DESCRIPTION contiene una descrizione delle caratteristiche di ogni cluster. È possibile esplorare queste colonne tramite SELECT FROM \<modello >. CONTENUTO istruzione DMX. Questa istruzione consente anche di esplorare i dati utilizzati per creare il modello di data mining. Per utilizzare questa istruzione è necessario che sia abilitato il drill-through nella struttura di data mining. Per altre informazioni sull'istruzione, vedere [SELECT FROM &#60;modello&#62;. I casi &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
 È inoltre possibile ottenere tutti gli stati di una colonna discreta utilizzando l'istruzione SELECT DISTINCT. Se ad esempio si esegue questa operazione su una colonna relativa al sesso, la query restituirà `male` e `female`.  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Esplorazione del contenuto dei modelli di data mining  
  
-   Restituzione dei case dall'origine dei dati utilizzata per il training dei modelli di data mining  
  
-   Esplorazione dei vari stati disponibili per una determinata colonna discreta  
  
## <a name="returning-the-content-of-a-mining-model"></a>Restituzione del contenuto di un modello di data mining  
 In questa lezione, Usa la [SELECT FROM &#60;modello&#62;. CONTENUTO &#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx) istruzione per restituire il contenuto del modello di clustering.  
  
 Di seguito è riportato un esempio generico del SELECT FROM \<modello >. Istruzione del contenuto:  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 La prima riga del codice definisce le colonne da restituire dal contenuto del modello di data mining, nonché il modello di data mining a cui sono associate:  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 La clausola .CONTENT accanto al nome del modello di data mining specifica che il contenuto restituito proviene dal modello di data mining. Per altre informazioni sulle colonne contenute nel modello di data mining, vedere [set di righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 È possibile utilizzare facoltativamente la riga finale del codice per filtrare i risultati restituiti dall'istruzione:  
  
```  
WHERE <where clause>  
```  
  
 Se ad esempio si desidera limitare i risultati della query ai soli cluster contenenti un numero elevato di case, è possibile aggiungere all'istruzione SELECT la clausola WHERE seguente:  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 Per altre informazioni sull'utilizzo dell'istruzione WHERE, vedere [selezionare &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>Per ottenere la restituzione del contenuto del modello di data mining di clustering  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico del SELECT FROM \<modello >. CONTENUTO istruzione nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    *  
    ```  
  
     È inoltre possibile sostituire * con un elenco di colonne contenute all'interno di [set di righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
4.  Sostituire quanto segue:  
  
    ```  
    [<mining model>]   
    ```  
  
     con:  
  
    ```  
    [Clustering]  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
6.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `SELECT_CONTENT.dmx`.  
  
7.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituisce il contenuto del modello di data mining.  
  
## <a name="use-drillthrough"></a>Utilizzo del drill-through  
 Il passaggio successivo consiste nell'utilizzo dell'istruzione di drill-through per ottenere un campionamento dei case utilizzati per il training del modello di data mining dell'albero delle decisioni. In questa lezione, Usa la [SELECT FROM &#60;modello&#62;. I casi &#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx) istruzione per restituire il contenuto del modello di albero delle decisioni.  
  
 Di seguito è riportato un esempio generico del SELECT FROM \<modello >. Istruzione case:  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 La prima riga del codice definisce le colonne da restituire dall'origine dei dati, nonché il modello di data mining in cui sono contenute:  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 La clausola .CASES specifica l'esecuzione di una query drill-through. Per utilizzare il drill-through è necessario che venga attivato durante la creazione del modello di data mining.  
  
 L'ultima riga del codice è facoltativa e specifica il nodo nel modello di data mining da cui si desidera ottenere i case:  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 Per altre informazioni sull'utilizzo dell'istruzione WHERE con IsInNode, vedere [SELECT FROM &#60;modello&#62;. I casi &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>Per ottenere la restituzione dei case utilizzati per il training del modello di data mining  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico del SELECT FROM \<modello >. Istruzione case nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    *  
    ```  
  
     È inoltre possibile sostituire * con un elenco di colonne contenute nell'origine dei dati, ad esempio [Bike Buyer]  
  
4.  Sostituire quanto segue:  
  
    ```  
    [<mining model>]   
    ```  
  
     con:  
  
    ```  
    [Decision Tree]  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
6.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `SELECT_DRILLTHROUGH.dmx`.  
  
7.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituisce i dati di origine utilizzati per il training del modello di data mining dell'albero delle decisioni.  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>Restituzione degli stati di una colonna discreta del modello di data mining  
 Il passaggio successivo consiste nell'utilizzo dell'istruzione SELECT DISTINCT per ottenere i vari stati possibili nella colonna specificata del modello di data mining.  
  
 Di seguito è riportato un esempio generico dell'istruzione SELECT DISTINCT:  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 La prima riga del codice definisce le colonne del modello di data mining per cui vengono restituiti gli stati:  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 È necessario includere DISTINCT affinché vengano restituiti tutti gli stati della colonna. Se si esclude DISTINCT, l'istruzione completa diventa una forma abbreviata di una stima e restituisce lo stato più probabile della colonna selezionata. Per altre informazioni, vedere [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>Per ottenere la restituzione degli stati di una colonna discreta  
  
1.  Nella **Esplora oggetti**, fare doppio clic sull'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], scegliere **nuova Query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico dell'istruzione SELECT DISTINCT nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    [<column,name>   
    ```  
  
     con:  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  Sostituire quanto segue:  
  
    ```  
    [<mining model>]   
    ```  
  
     con:  
  
    ```  
    [Decision Tree]  
    ```  
  
     L'istruzione completa dovrebbe risultare analoga alla seguente:  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  Nel **File** menu, fare clic su **Salva Dmxquery1.DMX**.  
  
6.  Nel **Salva con nome** della finestra di dialogo passare alla cartella appropriata e assegnare un nome di file `SELECT_DISCRETE.dmx`.  
  
7.  Sulla barra degli strumenti, scegliere il **Execute** pulsante.  
  
     La query restituisce gli stati possibili della colonna Bike Buyer.  
  
 Nella lezione successiva verrà utilizzato il modello di data mining dell'albero delle decisioni per stimare se i clienti potenziali diventeranno acquirenti di biciclette.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 5: L'esecuzione di query di stima](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
