---
title: Aggiungere espressioni ai vincoli di precedenza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence executables [Integration Services]
- precedence constraints [Integration Services], adding expressions
- adding expressions
- constrained executables [Integration Services]
- combining constraints
- expressions [Integration Services], constraints
ms.assetid: 5574d89a-a68e-4b84-80ea-da93305e5ca1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3b86869a2b5d2e1ecd93227355509170db2bd5c7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439668"
---
# <a name="add-expressions-to-precedence-constraints"></a>Aggiunta di espressioni ai vincoli di precedenza
  In un vincolo di precedenza è possibile utilizzare un'espressione per definire il vincolo tra due eseguibili: l'eseguibile con precedenza e l'eseguibile soggetto al vincolo. Gli eseguibili possono essere attività o contenitori. L'espressione può essere utilizzata da sola o in combinazione con il risultato dell'esecuzione dell'eseguibile con precedenza. Il risultato dell'esecuzione di un eseguibile può essere Success o Failure. Quando si configura il risultato dell'esecuzione di un vincolo di precedenza è possibile impostare il risultato dell'esecuzione su `Success`, `Failure` o `Completion`. `Success` richiede che l'esecuzione dell'eseguibile con precedenza venga completata correttamente, `Failure` richiede che l'esecuzione dell'eseguibile con precedenza non riesca e `Completion` indica che l'eseguibile soggetto al vincolo deve essere eseguito indipendentemente dall'esito dell'esecuzione dell'attività con precedenza. Per altre informazioni, vedere [Vincoli di precedenza](control-flow/precedence-constraints.md).  
  
 L'espressione, che deve restituire `True` o `False`, deve essere un'espressione di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] valida. e può utilizzare valori letterali, variabili di sistema e personalizzate, nonché le funzioni e gli operatori forniti dalla grammatica delle espressioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . L'espressione `@Count == SQRT(144) + 10`, ad esempio, utilizza la variabile `Count`, la funzione SQRT e gli operatori di uguaglianza (==) e di addizione (+). Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md).  
  
 Nella figura seguente le attività A e B sono collegate da un vincolo di precedenza che utilizza il risultato di un'esecuzione e un'espressione. Il valore del vincolo è impostato su `Success` e l'espressione è `@X >== @Z`. L'attività B, soggetta al vincolo, viene eseguita solo se l'attività A viene completata e il valore della variabile `X` è maggiore o uguale a quello della variabile `Z`.  
  
 ![Vincolo di precedenza tra due attività](media/mw-dts-03.gif "Vincolo di precedenza tra due attività")  
  
 Per collegare gli eseguibili è inoltre possibile utilizzare più vincoli di precedenza contenenti espressioni diverse. Nella figura seguente, ad esempio, le attività B e C sono collegate all'attività A da vincoli di precedenza che utilizzano risultati di esecuzione ed espressioni. I valori di entrambi i vincoli sono impostati su `Success.` Uno dei vincoli di precedenza include l'espressione `@X >== @Z`, mentre l'altro include l'espressione `@X < @Z`. A seconda dei valori assunti dalle variabili `X` e `Z`, verrà eseguita l'attività C o l'attività B.  
  
 ![Espressioni nei vincoli di precedenza](media/mw-dts-04.gif "Espressioni nei vincoli di precedenza")  
  
 Per aggiungere o modificare un'espressione, è possibile usare **Editor vincoli di precedenza** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] e la finestra Proprietà disponibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . La finestra Proprietà non è tuttavia in grado di verificare la sintassi delle espressioni.  
  
 Se un vincolo di precedenza include un'espressione, sull'area di progettazione delle scheda **Flusso di controllo** verrà visualizzata un'icona accanto al vincolo di precedenza e l'espressione verrà visualizzata nella descrizione comando di tale icona.  
  
## <a name="combining-execution-values-and-expressions"></a>Combinazione di valori di esecuzione ed espressioni  
 Nella tabella seguente vengono descritti gli effetti ottenuti combinando un vincolo su un valore di esecuzione e un'espressione in un vincolo precedenza.  
  
|Operazioni di valutazione|Valore restituito dal vincolo|Valore restituito dall'espressione|Esecuzione eseguibile soggetto al vincolo|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|Vincolo|True|N/D|True|  
|Vincolo|False|N/D|False|  
|Expression|N/D|True|True|  
|Expression|N/D|False|False|  
|Vincolo ed espressione|True|True|True|  
|Vincolo ed espressione|True|False|False|  
|Vincolo ed espressione|False|True|False|  
|Vincolo ed espressione|False|False|False|  
|Vincolo o espressione|True|True|True|  
|Vincolo o espressione|True|False|True|  
|Vincolo o espressione|False|True|True|  
|Vincolo o espressione|False|False|False|  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>Per aggiungere un'espressione a un vincolo di precedenza  
  
-   [Uso di un'espressione in un vincolo di precedenza](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
-   [Impostazione delle proprietà di un vincolo di precedenza](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
## <a name="external-resources"></a>Risorse esterne  
 Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com  
  
## <a name="see-also"></a>Vedere anche  
 [Più vincoli di precedenza](../../2014/integration-services/multiple-precedence-constraints.md)   
 [Vincoli di precedenza](control-flow/precedence-constraints.md)  
  
  
