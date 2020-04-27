---
title: Contenitore Ciclo For | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 991223c373113b465c3182f552e5f5d157efef9f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62831609"
---
# <a name="for-loop-container"></a>Contenitore Ciclo For
  Il contenitore Ciclo For definisce un flusso di controllo ripetuto all'interno di un pacchetto. L'implementazione del ciclo è simile alla struttura del ciclo **For** nei linguaggi di programmazione. A ogni ripetizione del ciclo il contenitore Ciclo For valuta un'espressione e ne ripete il flusso di lavoro finché tale espressione non restituisce `False`.  
  
 Per definire il ciclo, il contenitore Ciclo For usa gli elementi seguenti:  
  
-   Un'espressione di inizializzazione facoltativa che assegna valori ai contatori del ciclo.  
  
-   Un'espressione di valutazione che contiene l'espressione utilizzata per stabilire se il ciclo deve essere arrestato o continuare.  
  
-   Un'espressione di iterazione facoltativa che incrementa o decrementa il contatore del ciclo.  
  
 Nella figura seguente viene illustrato un contenitore Ciclo For con un'attività Invia messaggi. Se l'espressione di inizializzazione è `@Counter = 0`, l'espressione di valutazione è `@Counter < 4`e l'espressione di iterazione è `@Counter = @Counter + 1`, il ciclo si ripeterà quattro volte e verranno inviati quattro messaggi di posta elettronica.  
  
 ![Un contenitore Ciclo For ripete un'attività quattro volte](../media/ssis-forloop.gif "Un contenitore Ciclo For ripete un'attività quattro volte")  
  
 Le espressioni devono essere espressioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] valide.  
  
 Per creare le espressioni di inizializzazione e assegnazione, è possibile utilizzare l'operatore di assegnazione (=). In altre circostanze questo operatore non è supportato dalla grammatica delle espressioni di Integration Services, ma può essere utilizzato solo dai tipi di espressione di inizializzazione e assegnazione nel contenitore Ciclo For. Tutte le espressioni che usano l'operatore di assegnazione devono avere la sintassi `@Var = <expression>`, dove **Var** è una variabile di runtime ed \<expression> è un'espressione che segue le regole della sintassi delle espressioni di [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. L'espressione può includere le variabili, i valori letterali e tutti gli operatori e le funzioni supportati dalla grammatica delle espressioni di SSIS. L'espressione deve restituire un tipo di dati di cui è possibile eseguire il cast al tipo di dati della variabile.  
  
 Un contenitore Ciclo For può includere una sola espressione di valutazione, pertanto esegue tutti gli elementi del flusso di controllo per lo stesso numero di volte. Poiché un contenitore Ciclo For può includere altri contenitori Ciclo For, nei pacchetti è possibile compilare cicli nidificati e implementare loop complessi.  
  
 È possibile impostare una proprietà di transazione sul contenitore Ciclo For per definire una transazione per un subset del flusso di controllo del pacchetto. In questo modo è possibile gestire le transazioni con un livello di granularità superiore. Se ad esempio un contenitore Ciclo For ripete un flusso di controllo che aggiorna più volte i dati di una tabella, sarà possibile configurare il ciclo For e il relativo flusso di controllo per l'utilizzo di una transazione, in modo da assicurare che se non è possibile aggiornare correttamente tutti i dati, non ne verrà aggiornato alcuno. Per altre informazioni, vedere [Transazioni di Integration Services](../integration-services-transactions.md).  
  
## <a name="configuration-of-the-for-loop-container"></a>Configurazione del contenitore Ciclo For  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor ciclo For](../for-loop-editor.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione a livello di codice di queste proprietà, vedere la documentazione per la classe **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** nella Guida per gli sviluppatori.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni sulla configurazione di un contenitore Ciclo For, vedere gli argomenti seguenti.  
  
-   [Configurazione di un contenitore Ciclo For](for-loop-container.md)  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](control-flow.md)   
 [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md)  
  
  
