---
title: Impostare le proprietà di un vincolo di precedenza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b0c8d2eec40078e58b80170b37c4885b72ad2b8
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388119"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>Impostazione delle proprietà di un vincolo di precedenza
  Per impostare le proprietà dei vincoli di precedenza, è possibile utilizzare uno dei seguenti strumenti:  
  
-   La finestra di dialogo **Editor vincoli di precedenza** .  
  
-   La finestra Proprietà. Nella finestra Proprietà sono elencate le proprietà per la configurazione dei vincoli di precedenza non disponibili nella finestra di dialogo **Editor vincoli di precedenza** . ed è possibile specificare una descrizione e un nome del vincolo di precedenza, nonché configurare l'annotazione da visualizzare per il vincolo di precedenza nell'area di progettazione.  
  
 Nelle procedure seguenti viene descritta l'impostazione delle proprietà dei vincoli di precedenza tramite ognuno di questi strumenti.  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>Per impostare le proprietà di un vincolo di precedenza tramite Editor vincoli di precedenza  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Fare doppio clic sul vincolo di precedenza.  
  
     Verrà aperta la finestra di dialogo **Editor vincoli di precedenza** .  
  
5.  Nell'elenco a discesa **Operazione valutazione** selezionare un'operazione di valutazione.  
  
6.  Nel `Value` elenco a discesa selezionare il risultato dell'esecuzione dell'eseguibile con precedenza.  
  
7.  Se l'operazione di valutazione viene utilizzata un'espressione, nelle `Expression` casella, digitare un'espressione e fare clic su **Test** per valutare l'espressione.  
  
    > [!NOTE]  
    >  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
8.  Se per l'eseguibile soggetto al vincolo sono connessi più contenitori o attività, selezionare **AND logico** per specificare che devono restituire i risultati dell'esecuzione di tutti gli eseguibili con precedenza `true`. Selezionare **Logical OR** per specificare che deve restituire solo un risultato di esecuzione `true`.  
  
9. Scegliere **OK** per chiudere la finestra **Editor vincoli di precedenza**.  
  
10. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>Per impostare le proprietà di un vincolo di precedenza tramite la finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto da modificare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** . Nell'area di progettazione della scheda **Flusso di controllo** fare clic sul vincolo di precedenza con il pulsante destro del mouse e quindi scegliere **Proprietà**. Nella finestra Proprietà modificare i valori delle proprietà.  
  
4.  Nella finestra **Proprietà** impostare le proprietà di lettura/scrittura seguenti dei vincoli di precedenza:  
  
    |Proprietà di lettura/scrittura|Azione di configurazione|  
    |--------------------------|--------------------------|  
    |Descrizione|Specificare una descrizione.|  
    |EvalOp|Selezionare un'operazione di valutazione. Se il `Expression`, **ExpressionAndConstant**, o **ExpressionOrConstant** operazione è selezionata, è possibile specificare un'espressione.|  
    |Espressione|Se l'operazione di valutazione include un'espressione, specificare l'espressione. L'espressione deve restituire un valore booleano. Per altre informazioni sul linguaggio delle espressioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).|  
    |LogicalAnd|Impostare `LogicalAnd` per specificare se il vincolo di precedenza viene valutato insieme ad altri vincoli di precedenza, quando più eseguibili precedono e sono collegati all'eseguibile soggetto al|  
    |nome|Aggiornare il nome del vincolo di precedenza.|  
    |ShowAnnotation|Specificare il tipo di annotazione da utilizzare. Selezionare **Never** per disabilitare le annotazioni, **AsNeeded** per attivare le annotazioni su richiesta, **ConstraintName** per aggiungere automaticamente annotazioni usando il valore della proprietà Name, **ConstraintDescription** per aggiungere automaticamente annotazioni usando il valore della proprietà Description e **ConstraintOptions** per aggiungere automaticamente annotazioni usando i valori delle proprietà Value ed Expression.|  
    |Value|Se l'operazione di valutazione specificata nella proprietà EvalOP include un vincolo, selezionare il risultato dell'esecuzione dell'eseguibile vincolante.|  
  
5.  Chiudere la finestra Proprietà.  
  
6.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Vincoli di precedenza](control-flow/precedence-constraints.md)   
 [Connessione di attività e contenitori tramite un vincolo di precedenza predefinito](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Impostare il valore di un vincolo di precedenza tramite il Menu di scelta rapida](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Uso di un'espressione in un vincolo di precedenza](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
