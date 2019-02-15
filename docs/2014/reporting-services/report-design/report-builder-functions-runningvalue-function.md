---
title: Funzione RunningValue (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 02e670fd13f249e1278675b02097f4921dd41ebe
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285969"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>Funzione RunningValue (Generatore report e SSRS)
  Restituisce un'aggregazione parziale di tutti i valori numerici non Null specificati dall'espressione, valutata per l'ambito specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>Parametri  
 *expression*  
 Espressione su cui eseguire l'aggregazione, ad esempio `[Quantity]`.  
  
 *function*  
 (`Enum`) Nome della funzione di aggregazione da applicare all'espressione, ad esempio `Sum`. Tale funzione non può essere `RunningValue`, `RowNumber` o `Aggregate`.  
  
 *ambito*  
 (`String`) Costante di tipo stringa ovvero il nome di un set di dati, area dati o gruppo oppure valore Null (`Nothing` in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) tramite cui viene specificato il contesto in cui valutare l'aggregazione. Tramite `Nothing` viene specificato il contesto più esterno, generalmente il set di dati del report.  
  
## <a name="return-type"></a>Tipo restituito  
 Dipende dalla funzione di aggregazione specificata nel parametro *function* .  
  
## <a name="remarks"></a>Note  
 Il valore per `RunningValue` viene reimpostato su 0 per ogni nuova istanza dell'ambito. Se viene specificato un gruppo, il valore corrente viene reimpostato quando viene modificata l'espressione di raggruppamento. Se viene specificata un'area dati, il valore corrente viene reimpostato per ogni nuova istanza dell'area dati. Se viene specificato un set di dati, il valore corrente non viene reimpostato nell'intero set di dati.  
  
 `RunningValue` non può essere utilizzato in un filtro o un'espressione di ordinamento.  
  
 Il set di dati per il quale il valore corrente è calcolato deve avere lo stesso tipo di dati. Per convertire dati con più tipi di dati numerici nello stesso tipo di dati, usare funzioni di conversione come `CInt`, `CDbl` o `CDec`. Per altre informazioni, vedere [Funzioni di conversione del tipo](https://go.microsoft.com/fwlink/?LinkId=96142).  
  
 *Scope* non può essere un'espressione.  
  
 *Expression* può contenere chiamate alle funzioni di aggregazione nidificate con le eccezioni e le condizioni seguenti:  
  
-   Scope per le aggregazioni nidificate deve corrispondere o essere contenuto nell'ambito dell'aggregazione esterna. Per tutti gli ambiti distinti nell'espressione, un ambito deve essere in una relazione figlio con tutti gli altri ambiti.  
  
-   Scope per le aggregazioni nidificate non può essere il nome di un set di dati.  
  
-   *Espressione* non deve contenere `First`, `Last`, `Previous`, o `RunningValue` funzioni.  
  
-   *Expression* non deve contenere aggregazioni nidificate che specificano *recursive*.  
  
 Per calcolare il valore corrente del numero di righe, utilizzare `RowNumber`. Per altre informazioni, vedere [Funzione RowNumber &#40;Generatore report e SSRS&#41;](report-builder-functions-rownumber-function.md).  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Per altre informazioni sulle aggregazioni ricorsive, vedere [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="examples"></a>Esempi  
 L'esempio di codice seguente consente di ottenere una somma parziale del campo denominato `Cost` nell'ambito più esterno, che corrisponde al set di dati.  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 L'esempio di codice seguente consente di ottenere una somma parziale del campo denominato `Score` nel set di dati denominato `DataSet1`.  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 L'esempio di codice seguente consente di ottenere una somma parziale del campo denominato `Traffic Charges` nell'ambito più esterno.  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
