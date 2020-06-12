---
title: Eseguire una query sui parametri utilizzati per creare un modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: ce7719e0-6127-4d9c-a753-0e0a3db065e1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1d24d3316275e649a62e2c66d01e683a20b7a640
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520587"
---
# <a name="query-the-parameters-used-to-create-a-mining-model"></a>Eseguire query sui parametri utilizzati per creare un modello di data mining
  La composizione di un modello di data mining non è interessata solo dai case di training, ma anche dai parametri impostati alla creazione del modello. Pertanto, è possibile recuperare le impostazioni dei parametri di un modello esistente per comprendere meglio il comportamento dello stesso. Il recupero dei parametri può essere utile anche per documentare una determinata versione del modello.  
  
 Per trovare i parametri utilizzati alla creazione del modello, creare una query su uno dei set di righe dello schema del modello di data mining. In [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]questi set di righe dello schema sono esposti come set di viste di sistema su cui è possibile eseguire query in modo semplice usando la sintassi Transact-SQL. In questa procedura viene descritto come creare una query che restituisce i parametri utilizzati per creare il modello di data mining specificato.  
  
### <a name="to-open-a-query-window-for-a-schema-rowset-query"></a>Per aprire una finestra Query per una query sul set di righe dello schema  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente il modello su cui eseguire la query.  
  
2.  Fare clic con il pulsante destro del mouse sul nome dell'istanza, scegliere **Nuova query**, quindi **DMX**.  
  
    > [!NOTE]  
    >   È anche possibile creare una query su un modello di data mining tramite il modello **MDX** .  
  
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
 Nel codice seguente viene restituito un elenco dei parametri utilizzati per creare il modello di data mining compilato nell' [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md) Questi parametri includono i valori espliciti relativi alle impostazioni predefinite utilizzate dai servizi di data mining disponibili dai provider nel server.  
  
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
 [Attività e procedure relative alle query di data mining](data-mining-query-tasks-and-how-tos.md)   
 [Query di data mining](data-mining-queries.md)  
  
  
