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
ms.openlocfilehash: f68a66e778d44059a83ca6eca3cee35b4dffca9c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892758"
---
# <a name="functions-dmx"></a>Funzioni (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando si utilizza DMX (Data Mining Extensions) per eseguire query sugli [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]oggetti in, è possibile utilizzare le funzioni per restituire più informazioni rispetto ai soli valori delle colonne del modello di data mining o del set di dati di input. È ad esempio possibile utilizzare query DMX per ottenere sia il valore stimato di una colonna, sia la probabilità che tale stima sia corretta. Oltre alle funzioni DMX è possibile utilizzare anche stored procedure e funzioni di Microsoft Visual Basic, Applications Edition (VBA) e Microsoft Excel.  
  
## <a name="dmx-functions"></a>Funzioni DMX  
 È possibile utilizzare funzioni DMX per eseguire le attività seguenti:  
  
-   Restituire stime.  
  
-   Restituire statistiche relative a una stima, quali probabilità e supporto.  
  
-   Filtrare i risultati di una query.  
  
-   Riordinare un'espressione di tabella.  
  
 La maggior parte delle funzioni DMX restituisce un valore scalare, ad esempio il supporto di una stima, ma alcune restituiscono un risultato tabulare. Ad esempio, la funzione PredictHistogram restituisce una tabella che contiene il supporto e la probabilità per ogni stato della colonna stimabile specificata. I risultati vengono visualizzati come una nuova colonna di tabella.  
  
 **Per ulteriori informazioni: funzioni di** [stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [data Mining Extensions &#40;DMX&#41; Function Reference](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funzioni di Visual Basic, Applications Edition (VBA) e di Excel  
 Oltre alle funzioni DMX, dalle istruzioni DMX è possibile chiamare anche un'ampia gamma di funzioni di Excel e VBA. È ad esempio possibile utilizzare la funzione lCase per modificare la modalità di visualizzazione della colonna Attribute_Name nel contenuto del modello TM_Decision_Tree. come illustrato nell'esempio di codice seguente.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Se la stessa funzione è presente sia in VBA che in Excel, è necessario anteporre il nome della funzione nell'istruzione DMX con **VBA** o **Excel**. specificando ad esempio `VBA!Log` o `Excel!Log`. Se la funzione di Excel o VBA da utilizzare esiste anche in DMX o MDX (Multidimensional Expressions), oppure contiene un simbolo di dollaro ($), sarà necessario utilizzare le parentesi quadre ([]) come caratteri di escape. Per chiamare la funzione può essere ad esempio necessario specificare `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Stored procedure  
 È possibile utilizzare linguaggi di programmazione CLR (Common Language Runtime) per creare stored procedure in grado di estendere le funzionalità di DMX. Un modello di data mining dell'albero di regressione, ad esempio, restituisce coefficienti, ad esempio A, B e così via, che descrivono l'equazione di regressione, ma il modello non restituisce l'equazione stessa, ad esempio + BX = y. È tuttavia possibile creare una stored procedure che utilizza l'oggetto modello di data mining per navigare nello schema del contenuto e restituire l'equazione di regressione come output. Un'istruzione DMX può pertanto restituire un elenco di equazioni di regressione nell'ambito dei risultati di una query.  
  
 **Per ulteriori informazioni: gestione degli assembly di** [modelli multidimensionali](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-assemblies-management)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
