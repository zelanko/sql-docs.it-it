---
title: Utilizzare un'espressione in un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- components [Integration Services], data flow
- expressions [Integration Services], data flow components
ms.assetid: 9181b998-d24a-41fb-bb3c-14eee34f910d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bc9f6c28e775cdbd21806172d7074e655fdd1545
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054815"
---
# <a name="use-an-expression-in-a-data-flow-component"></a>Utilizzo di un'espressione in un componente flusso di dati
  In questo argomento viene descritta la procedura per l'aggiunta di un'espressione nella trasformazione Suddivisione condizionale o Colonna derivata. La trasformazione Suddivisione condizionale utilizza espressioni per definire le condizioni che dirigono le righe di dati all'output della trasformazione, mentre la trasformazione Colonna derivata utilizza espressioni per definire i valori assegnati alle colonne.  
  
 Per implementare un'espressione in una trasformazione, è necessario che il pacchetto includa almeno un'attività Flusso di dati e un'origine. Per informazioni sull'aggiunta di questi elementi ai pacchetti, vedere gli argomenti seguenti:  
  
-   [Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
    
  
-   [Aggiunta o eliminazione di un componente in un flusso di dati](data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
-   [Connessione di componenti in un flusso di dati](data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-create-an-expression"></a>Per creare un'espressione  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** e quindi sull'attività Flusso di dati contenente il flusso di dati in cui si vuole implementare un'espressione.  
  
4.  Fare clic sulla scheda **Flusso di dati** e trascinare una trasformazione Suddivisione condizionale o Colonna derivata dalla **casella degli strumenti** all'area di progettazione.  
  
5.  Trascinare il connettore verde dall'origine o trasformazione alla trasformazione Suddivisione condizionale o Colonna derivata.  
  
6.  Fare doppio clic sulla trasformazione. Verrà visualizzata la finestra di dialogo corrispondente.  
  
7.  Nel riquadro di sinistra espandere il nodo **Variabili** in modo da visualizzare le variabili definite dall'utente e di sistema. Espandere anche il nodo **Colonne** in modo da visualizzare le colonne di input della trasformazione.  
  
8.  Nel riquadro di destra espandere i nodi **Funzioni matematiche**, **Funzioni per i valori stringa**, **Funzioni di data/ora**, **Funzioni NULL**, **Cast di tipo**e **Operatori** per accedere alle funzioni, ai cast e agli operatori del linguaggio delle espressioni.  
  
9. A seconda della trasformazione, compilare un'espressione in uno dei modi seguenti:  
  
    -   Nella finestra di dialogo **Editor trasformazione Suddivisione condizionale** trascinare variabili, colonne, funzioni, operatori e cast nella colonna **Condizione** . In alternativa, è possibile digitare l'espressione direttamente nella colonna **Condizione** .  
  
    -   Nella finestra di dialogo **Editor trasformazione Colonna derivata** trascinare variabili, colonne, funzioni, operatori e cast nella colonna **Espressione** . In alternativa, è possibile digitare l'espressione direttamente nella colonna **Espressione** .  
  
        > [!NOTE]  
        >  Quando lo stato attivo viene rimosso dalla colonna **Condizione** o **Espressione** , il testo dell'espressione potrebbe essere evidenziato per indicare che la sintassi dell'espressione non è corretta.  
  
10. Fare clic su **OK** per chiudere la finestra di dialogo.  
  
    > [!NOTE]  
    >  Se l'espressione non è valida, viene visualizzato un avviso che evidenzia gli errori di sintassi.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)   
 [Conditional Split Transformation](data-flow/transformations/conditional-split-transformation.md)   
 [Derived Column Transformation](data-flow/transformations/derived-column-transformation.md)   
 [Attività Flusso di dati](control-flow/data-flow-task.md)   
 [Flusso di dati](data-flow/data-flow.md)  
  
  
