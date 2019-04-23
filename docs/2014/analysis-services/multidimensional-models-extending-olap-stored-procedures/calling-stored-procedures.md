---
title: Chiamata di Stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- stored procedures [Analysis Services], calling
- MDX queries [Analysis Services]
- CALL statement
ms.assetid: 96a9660d-875b-4ee4-b339-90020b1d9895
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55569f23ae943e96a495905434bb0d39f2796a63
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157889"
---
# <a name="calling-stored-procedures"></a>Chiamata di stored procedure
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
 È possibile chiamare stored procedure al di fuori del contesto di una query MDX utilizzando l'istruzione MDX `Call`.  
  
 È possibile utilizzare questo metodo per creare un'istanza degli effetti collaterali di una query archiviata oppure per l'applicazione per ottenere i risultati di una query archiviata. L'istruzione `Call` viene in genere utilizzata per eseguire tramite AMO (Analysis Management Objects) funzioni amministrative che non restituiscono risultati. Ad esempio, per chiamare una stored procedure è possibile utilizzare i comandi seguenti:  
  
```  
Call MyStoredProcedure(a,b,c)  
```  
  
 Il solo tipo supportato restituito da una stored procedure in un'istruzione `Call` è un set di righe. La serializzazione di un set di righe viene definita tramite XML for Analysis. Se una stored procedure in un'istruzione `Call` restituisce qualsiasi altro tipo, viene ignorata e non viene restituita in XML all'applicazione chiamante. Per ulteriori informazioni sui set di righe di schema di XML for Analysis, vedere l'argomento corrispondente.  
  
 Se una stored procedure restituisce un set di righe .NET, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte il risultato nel server in un set di righe XML for Analysis. Il set di righe XML for Analysis viene sempre restituito da una stored procedure nella funzione `Call`. Se un set di dati contiene caratteristiche che non possono essere espresse nel set di righe di XML for Analysis, si verifica un errore.  
  
 Le stored procedure che restituiscono valori void, ad esempio subroutine di Visual Basic, possono essere utilizzate con la parola chiave CALL. Se ad esempio si desidera utilizzare la funzione MyVoidFunction() in un'istruzione MDX, è necessario utilizzare la sintassi seguente:  
  
```  
CALL(MyVoidFunction)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di assembly di modelli multidimensionali](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definizione delle stored procedure](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
