---
title: 'Lezione 4: esplorazione dei modelli di data mining Bike Buyer | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63070891"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>Lezione 4: Esplorazione dei modelli di data mining Bike Buyer
  In questa lezione verrà utilizzata l'istruzione [Select (DMX)](/sql/dmx/select-dmx) per esplorare il contenuto dei modelli di data mining di clustering e di albero delle decisioni creati nella [lezione 2: aggiunta di modelli di data mining alla struttura di data mining predittiva](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md).  
  
 Le colonne contenute in un modello di data mining non sono quelle definite dalla struttura di data mining ma sono un set specifico di colonne che descrivono le tendenze e gli schemi individuati dall'algoritmo. Queste colonne del modello di data mining sono descritte nel set di righe dello schema [DMSCHEMA_MINING_MODEL_CONTENT set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset) . La colonna MODEL_NAME nel set di righe dello schema del contenuto, ad esempio, contiene il nome del modello di data mining. Per un modello di data mining di clustering, la colonna NODE_CAPTION contiene il nome di ogni cluster e la colonna NODE_DESCRIPTION contiene una descrizione delle caratteristiche di ogni cluster. Per esplorare queste colonne, è possibile usare l'> \<seleziona da modello. Istruzione CONTENT in DMX. Questa istruzione consente anche di esplorare i dati utilizzati per creare il modello di data mining. Per utilizzare questa istruzione è necessario che sia abilitato il drill-through nella struttura di data mining. Per ulteriori informazioni sull'istruzione, vedere [SELECT FROM &#60;model&#62;. CASI &#40;&#41;DMX ](/sql/dmx/select-from-model-content-dmx).  
  
 È inoltre possibile ottenere tutti gli stati di una colonna discreta utilizzando l'istruzione SELECT DISTINCT. Se ad esempio si esegue questa operazione su una colonna relativa al sesso, la query restituirà `male` e `female`.  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione verranno eseguite le attività seguenti:  
  
-   Esplorazione del contenuto dei modelli di data mining  
  
-   Restituzione dei case dall'origine dei dati utilizzata per il training dei modelli di data mining  
  
-   Esplorazione dei vari stati disponibili per una determinata colonna discreta  
  
## <a name="returning-the-content-of-a-mining-model"></a>Restituzione del contenuto di un modello di data mining  
 In questa lezione si utilizzerà il [modello di &#60;di selezione da&#62;. CONTENT &#40;istruzione DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx) per restituire il contenuto del modello di clustering.  
  
 Di seguito è riportato un esempio generico di SELECT FROM \<Model>. Istruzione CONTENT:  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 La prima riga del codice definisce le colonne da restituire dal contenuto del modello di data mining, nonché il modello di data mining a cui sono associate:  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 La clausola .CONTENT accanto al nome del modello di data mining specifica che il contenuto restituito proviene dal modello di data mining. Per ulteriori informazioni sulle colonne contenute nel modello di data mining, vedere [DMSCHEMA_MINING_MODEL_CONTENT set di righe](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 È possibile utilizzare facoltativamente la riga finale del codice per filtrare i risultati restituiti dall'istruzione:  
  
```  
WHERE <where clause>  
```  
  
 Se ad esempio si desidera limitare i risultati della query ai soli cluster contenenti un numero elevato di case, è possibile aggiungere all'istruzione SELECT la clausola WHERE seguente:  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 Per ulteriori informazioni sull'utilizzo dell'istruzione WHERE, vedere [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>Per ottenere la restituzione del contenuto del modello di data mining di clustering  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico della> SELECT FROM \<Model. Istruzione CONTENT nella query vuota.  
  
3.  Sostituire quanto segue:  
  
    ```  
    <select list>   
    ```  
  
     con:  
  
    ```  
    *  
    ```  
  
     È inoltre possibile sostituire * con un elenco di tutte le colonne contenute nel set di [righe DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
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
  
5.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
6.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `SELECT_CONTENT.dmx`il nome.  
  
7.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
     La query restituisce il contenuto del modello di data mining.  
  
## <a name="use-drillthrough"></a>Utilizzo del drill-through  
 Il passaggio successivo consiste nell'utilizzo dell'istruzione di drill-through per ottenere un campionamento dei case utilizzati per il training del modello di data mining dell'albero delle decisioni. In questa lezione si utilizzerà il [modello di &#60;di selezione da&#62;. Case &#40;istruzione DMX&#41;](/sql/dmx/select-from-model-content-dmx) per restituire il contenuto del modello di albero delle decisioni.  
  
 Di seguito è riportato un esempio generico di SELECT FROM \<Model>. Istruzione CASEs:  
  
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
  
 Per ulteriori informazioni sull'utilizzo dell'istruzione WHERE con IsInNode, vedere [SELECT FROM &#60;model&#62;. CASI &#40;&#41;DMX ](/sql/dmx/select-from-model-content-dmx).  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>Per ottenere la restituzione dei case utilizzati per il training del modello di data mining  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
     Verrà avviato l'editor di query con una nuova query vuota.  
  
2.  Copiare l'esempio generico della> SELECT FROM \<Model. Istruzione CASEs nella query vuota.  
  
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
  
5.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
6.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `SELECT_DRILLTHROUGH.dmx`il nome.  
  
7.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
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
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]mouse sull'istanza di, scegliere **nuova query**, quindi fare clic su **DMX**.  
  
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
  
5.  Scegliere **Salva DMXQuery1. DMX con nome**dal menu **file** .  
  
6.  Nella finestra di dialogo **Salva con** nome individuare la cartella appropriata e assegnare al file `SELECT_DISCRETE.dmx`il nome.  
  
7.  Sulla barra degli strumenti fare clic sul pulsante **Esegui** .  
  
     La query restituisce gli stati possibili della colonna Bike Buyer.  
  
 Nella lezione successiva verrà utilizzato il modello di data mining dell'albero delle decisioni per stimare se i clienti potenziali diventeranno acquirenti di biciclette.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 5: Esecuzione di query di stima](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
