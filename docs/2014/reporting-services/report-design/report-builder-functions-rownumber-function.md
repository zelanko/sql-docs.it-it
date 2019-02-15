---
title: Funzione RowNumber (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 27aaffc85ee01f2645b9bb590aa7816d2fa01f71
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292899"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>Funzione RowNumber (Generatore report e SSRS)
  Restituisce il conteggio parziale del numero di righe per l'ambito specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ambito*  
 (`String`) Nome di un set di dati, area dati o gruppo oppure valore Null (`Nothing` in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) tramite cui viene specificato il contesto in cui valutare il numero di righe. Tramite `Nothing` viene specificato il contesto più esterno, generalmente il set di dati del report.  
  
## <a name="remarks"></a>Note  
 `RowNumber` Restituisce un valore corrente del conteggio delle righe all'interno dell'ambito specificato, proprio come [RunningValue](report-builder-functions-runningvalue-function.md) restituisce il valore corrente di una funzione di aggregazione. Durante la definizione di un ambito, si specifica quando reimpostare il conteggio delle righe su 1.  
  
 *scope* non può essere un'espressione. Il parametro*scope* deve essere un ambito contenitore. I tipici ambiti, dal contenuto più esterno fino al più interno, sono set di dati di report, aree dati, gruppi di righe o di colonne.  
  
 Per incrementare i valori nelle colonne, specificare un ambito che corrisponde al nome di un gruppo di colonne. Per incrementare i numeri verso il basso delle righe, specificare un ambito che corrisponde al nome di un gruppo di righe.  
  
> [!NOTE]  
>  Non è possibile includere aggregazioni che specificano sia un gruppo di righe che un gruppo di colonne in un'unica espressione.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Esempio di codice  
 Di seguito è riportata un'espressione che è possibile usare per la proprietà `BackgroundColor` della riga di dettaglio di un'area dati Tablix per alternare il colore di tali righe per ogni gruppo, sempre a partire dal bianco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
