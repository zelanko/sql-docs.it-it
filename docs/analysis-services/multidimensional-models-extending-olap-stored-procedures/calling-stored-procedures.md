---
title: Chiamata di Stored procedure | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a0bdf517f2845e28a9d3520034d9de16ff65a25e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181161"
---
# <a name="calling-stored-procedures"></a>Chiamata di stored procedure
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile chiamare stored procedure nel server o da un'applicazione client. In entrambi i casi le stored procedure vengono sempre eseguite nel server, nel contesto del server o di un database. Non sono richieste autorizzazioni speciali per eseguire una stored procedure. Dopo che una stored procedure viene aggiunta da un assembly al contesto del server o del database, qualsiasi utente può eseguire la stored procedure purché il ruolo di quell'utente consenta le operazioni eseguite dalla stored procedure.  
  
 La chiamata di una stored procedure in MDX viene eseguita allo stesso modo della chiamata di una funzione MDX intrinseca. Per una stored procedure che non prevede parametri, vengono utilizzati il nome della stored procedure e una coppia vuota di parentesi:  
  
```  
MyStoredProcedure()  
```  
  
 Se la stored procedure utilizza uno o più parametri, i parametri vengono specificati in ordine separati da virgole. Nell'esempio seguente viene illustrata una stored procedure di esempio con tre parametri:  
  
```  
MyStoredProcedure("Parameter1", 2, 800)  
```  
  
## <a name="calling-stored-procedures-in-mdx-queries"></a>Chiamata di stored procedure in query MDX  
 In tutte le query MDX le stored procedure devono restituire il tipo sintatticamente corretto richiesto da un'espressione MDX. In caso contrario, si verifica un errore MDX. Nell'esempio seguente vengono illustrate stored procedure che restituiscono un set, un membro e il risultato di un'operazione matematica.  
  
### <a name="returning-a-set"></a>Restituzione di un set  
 Negli esempi seguenti viene implementata una stored procedure chiamata MySproc che restituisce un set. Nel primo esempio MySproc restituisce il set direttamente nell'espressione SELECT. Nei due esempi successivi MySproc restituisce il set come un argomento delle funzioni Crossjoin e DrilldownLevel.  
  
```  
SELECT MySetProcedure(a,b,c) ON 0 FROM Sales  
SELECT Crossjoin(MySetProcedure(a,b,c)) ON 0 FROM Sales  
SELECT DrilldownLevel(MySetProcedure(a,b,c)) ON 0 FROM Sales  
```  
  
### <a name="returning-a-member"></a>Restituzione di un membro  
 Nell'esempio seguente viene visualizzata una funzione MySproc che restituisce un membro:  
  
```  
SELECT Descendants(MySproc(a,b,c),3) ON 0 FROM Sales  
```  
  
### <a name="returning-the-result-of-a-math-operation"></a>Restituzione del risultato di un'operazione matematica  
  
```  
SELECT Country.Members on 0, MySproc(Measures.Sales) ON 1 FROM Sales  
```  
  
## <a name="calling-stored-procedures-with-the-call-statement"></a>Chiamata di stored procedure con l'istruzione Call  
 Le stored procedure possono essere chiamate all'esterno del contesto di una query MDX utilizzando MDX **chiamare** istruzione.  
  
 È possibile utilizzare questo metodo per creare un'istanza degli effetti collaterali di una query archiviata oppure per l'applicazione per ottenere i risultati di una query archiviata. Un utilizzo comune della **chiamare** istruzione, è possibile utilizzare oggetti AMO (Analysis Management) per eseguire funzioni amministrative che non è un valore restituito. Ad esempio, per chiamare una stored procedure è possibile utilizzare i comandi seguenti:  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 L'unico tipo supportato restituito dalla stored procedure in un **chiamare** istruzione è un set di righe. La serializzazione di un set di righe viene definita tramite XML for Analysis. Se una stored procedure in un **chiamare** istruzione restituisce qualsiasi altro tipo, viene ignorata e non restituito in XML all'applicazione chiamante. Per ulteriori informazioni sui set di righe di schema di XML for Analysis, vedere l'argomento corrispondente.  
  
 Se una stored procedure restituisce un set di righe .NET, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte il risultato nel server in un set di righe XML for Analysis. Il codice XML per set di righe Analysis viene sempre restituito da una stored procedure nel **chiamare** (funzione). Se un set di dati contiene caratteristiche che non possono essere espresse nel set di righe di XML for Analysis, si verifica un errore.  
  
 Le stored procedure che restituiscono valori void, ad esempio subroutine di Visual Basic, possono essere utilizzate con la parola chiave CALL. Se ad esempio si desidera utilizzare la funzione MyVoidFunction() in un'istruzione MDX, è necessario utilizzare la sintassi seguente:  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
