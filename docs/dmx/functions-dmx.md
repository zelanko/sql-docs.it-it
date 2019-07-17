---
title: Funzioni (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32cf59ea3ca8c7f153170881ac5eb970e50c90b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076408"
---
# <a name="functions-dmx"></a>Funzioni (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando si usa Data Mining Extensions (DMX) agli oggetti di query nel [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è possibile utilizzare funzioni per ottenere altre informazioni oltre solo i valori delle colonne nel modello di data mining o set di dati di input. È ad esempio possibile utilizzare query DMX per ottenere sia il valore stimato di una colonna, sia la probabilità che tale stima sia corretta. Oltre alle funzioni DMX è possibile utilizzare anche stored procedure e funzioni di Microsoft Visual Basic, Applications Edition (VBA) e Microsoft Excel.  
  
## <a name="dmx-functions"></a>Funzioni DMX  
 È possibile utilizzare funzioni DMX per eseguire le attività seguenti:  
  
-   Restituire stime.  
  
-   Restituire statistiche relative a una stima, quali probabilità e supporto.  
  
-   Filtrare i risultati di una query.  
  
-   Riordinare un'espressione di tabella.  
  
 La maggior parte delle funzioni DMX restituisce un valore scalare, ad esempio il supporto di una stima, ma alcune restituiscono un risultato tabulare. Ad esempio, la funzione PredictHistogram restituisce una tabella che contiene il supporto e probabilità per ogni stato della colonna stimabile specificata. I risultati vengono visualizzati come una nuova colonna di tabella.  
  
 **Per altre informazioni:** [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [estensioni Data Mining per i dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funzioni di Visual Basic, Applications Edition (VBA) e di Excel  
 Oltre alle funzioni DMX, dalle istruzioni DMX è possibile chiamare anche un'ampia gamma di funzioni di Excel e VBA. Ad esempio, è possibile usare la funzione lCase per modificare la modalità di visualizzazione nella colonna Attribute_Name nel contenuto del modello TM_Decision_Tree. come illustrato nell'esempio di codice seguente.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Se la stessa funzione esiste in VBA ed Excel, è necessario anteporre il nome della funzione nell'istruzione DMX con uno **VBA** oppure **Excel**. specificando ad esempio `VBA!Log` o `Excel!Log`. Se la funzione di Excel o VBA da utilizzare esiste anche in DMX o MDX (Multidimensional Expressions), oppure contiene un simbolo di dollaro ($), sarà necessario utilizzare le parentesi quadre ([]) come caratteri di escape. Per chiamare la funzione può essere ad esempio necessario specificare `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Stored procedure  
 È possibile utilizzare linguaggi di programmazione CLR (Common Language Runtime) per creare stored procedure in grado di estendere le funzionalità di DMX. Ad esempio, un modello di data mining dell'albero di regressione restituisce coefficienti, ad esempio A, B e così via, che descrivono l'equazione di regressione, ma il modello non viene restituito l'equazione vera e propria, ad esempio un + Bx = y. È tuttavia possibile creare una stored procedure che utilizza l'oggetto modello di data mining per navigare nello schema del contenuto e restituire l'equazione di regressione come output. Un'istruzione DMX può pertanto restituire un elenco di equazioni di regressione nell'ambito dei risultati di una query.  
  
 **Per altre informazioni:** [Gestione di assembly di modelli multidimensionali](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
