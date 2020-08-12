---
title: Funzione CountRows (Generatore report) | Microsoft Docs
description: Informazioni sulla funzione CountRows, che restituisce il numero di righe in un ambito specificato, incluse le righe con valori Null.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 81b82f0d0d01dec7e3302eb32e3422f527f02064
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034925"
---
# <a name="report-builder-functions---countrows-function"></a>Funzioni di Generatore report - Funzione CountRows
  Restituisce il numero di righe nell'ambito specificato, incluse le righe con valori Null.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ambito*  
 (**String**) Nome di un set di dati, area dati o gruppo che contiene gli elementi del report da conteggiare.  
  
 *ricorsivi*  
 (**Enumerated Type**) Facoltativo. **Simple** (impostazione predefinita) o **RdlRecursive**. Specifica se eseguire l'aggregazione in modo ricorsivo.  
  
## <a name="return-type"></a>Tipo restituito  
 Restituisce un valore **Integer**.  
  
## <a name="remarks"></a>Osservazioni  
 **CountRows** conteggia tutte le righe nell'ambito specificato, incluse le righe con valori Null.  
  
 Il valore di *scope* non può essere un'espressione e deve fare riferimento all'ambito corrente o a un ambito di contenuto.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Per altre informazioni sulle aggregazioni ricorsive, vedere [Creazione di gruppi di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente è illustrata un'espressione che calcola il numero di righe in un gruppo di righe denominato `GroupbyCategory` (in base all'espressione `[Category]`).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
