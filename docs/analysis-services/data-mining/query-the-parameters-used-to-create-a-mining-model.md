---
title: Eseguire query sui parametri usati per creare un modello di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df2eb8317f90a96b35fc886e2158000e0f57d09d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62469498"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>Eseguire query sui parametri utilizzati per creare un modello di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La composizione di un modello di data mining non è interessata solo dai case di training, ma anche dai parametri impostati alla creazione del modello. Pertanto, è possibile recuperare le impostazioni dei parametri di un modello esistente per comprendere meglio il comportamento dello stesso. Il recupero dei parametri può essere utile anche per documentare una determinata versione del modello.  
  
 Per trovare i parametri utilizzati alla creazione del modello, creare una query su uno dei set di righe dello schema del modello di data mining. Questi set di righe dello schema sono esposti come set di viste di sistema che è possibile eseguire facilmente query tramite la sintassi Transact-SQL. In questa procedura viene descritto come creare una query che restituisce i parametri utilizzati per creare il modello di data mining specificato.  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>Per aprire una finestra Query per una query sul set di righe dello schema  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente il modello su cui eseguire la query.  
  
2.  Fare clic con il pulsante destro del mouse sul nome dell'istanza, scegliere **Nuova query**, quindi **DMX**.  
  
    > [!NOTE]  
    >  È anche possibile creare una query su un modello di data mining tramite il modello **MDX** .  
  
3.  Se l'istanza contiene più database, selezionare quello che contiene il modello su cui eseguire la query dall'elenco **Database disponibili** nella barra degli strumenti.  
  
### <a name="to-return-model-parameters-for-an-existing-mining-model"></a>Per restituire i parametri di un modello di data mining esistente  
  
1.  Nel riquadro Query DMX digitare o incollare il testo seguente:  
  
    ```  
    SELECT MINING_PARAMETERS  
    FROM $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = ''  
    ```  
  
2.  In Esplora oggetti selezionare il modello di data mining desiderato, quindi trascinarlo nel riquadro Query DMX, tra le virgolette singole.  
  
3.  Premere F5 oppure fare clic su **Esegui**.  
  
## <a name="example"></a>Esempio  
 Nel codice seguente viene restituito un elenco dei parametri utilizzati per creare il modello di data mining compilato nell' [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c) Questi parametri includono i valori espliciti relativi alle impostazioni predefinite utilizzate dai servizi di data mining disponibili dai provider nel server.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
 Nell'esempio di codice vengono restituiti i parametri seguenti per il modello di clustering:  
  
 Risultati dell'esempio:  
  
 MINING_PARAMETERS  
  
 CLUSTER_COUNT=10,CLUSTER_SEED=0,CLUSTERING_METHOD=1,MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_STATES=100,MINIMUM_SUPPORT=1,MODELLING_CARDINALITY=10,SAMPLE_SIZE=50000,STOPPING_TOLERANCE=10  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alle query di data mining](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
