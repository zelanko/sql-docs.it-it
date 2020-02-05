---
title: Funzione RowNumber (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e918a674b48eeb34fad7ea660b7e907fc9dcb44b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65577183"
---
# <a name="report-builder-functions---rownumber-function"></a>Funzioni di Generatore report - Funzione RowNumber
  Restituisce il conteggio parziale del numero di righe per l'ambito specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ambito*  
 (**String**) Nome di un set di dati, area dati o gruppo oppure valore Null (**Nothing** in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) che specifica il contesto in cui valutare il numero di righe. Tramite**Nothing** viene specificato il contesto più esterno, generalmente il set di dati del report.  
  
## <a name="remarks"></a>Osservazioni  
 **RowNumber** restituisce il valore corrente del conteggio di righe all'interno dell'ambito specificato, così come [RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md) restituisce il valore corrente di una funzione di aggregazione. Durante la definizione di un ambito, si specifica quando reimpostare il conteggio delle righe su 1.  
  
 *scope* non può essere un'espressione. Il parametro*scope* deve essere un ambito contenitore. I tipici ambiti, dal contenuto più esterno fino al più interno, sono set di dati di report, aree dati, gruppi di righe o di colonne.  
  
 Per incrementare i valori nelle colonne, specificare un ambito che corrisponde al nome di un gruppo di colonne. Per incrementare i numeri verso il basso delle righe, specificare un ambito che corrisponde al nome di un gruppo di righe.  
  
> [!NOTE]  
>  Non è possibile includere aggregazioni che specificano sia un gruppo di righe che un gruppo di colonne in un'unica espressione.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Di seguito è riportata un'espressione che è possibile usare per la proprietà **BackgroundColor** della riga di dettaglio di un'area dati Tablix per alternare il colore di tali righe per ogni gruppo, sempre a partire dal bianco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
