---
description: RollupChildren (MDX)
title: RollupChildren (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fb4e3552b5c5f5a708a70754d816ab1a78008248
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341317"
---
# <a name="rollupchildren-mdx"></a>RollupChildren (MDX)


  Restituisce un valore generato tramite il rollup dei valori degli elementi figlio del membro indicato, utilizzando l'operatore unario specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>Argomenti  
 *Member_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un membro.  
  
 *Unary_Operator*  
 Espressione stringa valida che specifica un operatore unario.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **RollupChildren** esegue il rollup dei valori degli elementi figlio del membro specificato utilizzando l'operatore unario specificato.  
  
 Nella tabella seguente vengono descritti gli operatori unari validi per questa funzione.  
  
|Operatore|Risultato|  
|--------------|------------|  
|**+**|totale = totale + membro figlio corrente|  
|**-**|totale = totale - membro figlio corrente|  
|**\***|totale = totale * membro figlio corrente|  
|**/**|totale = totale / membro figlio corrente|  
|**%**|totale = (totale / membro figlio corrente) * 100|  
|**~**|Il membro figlio non viene utilizzato nel rollup e il valore corrispondente viene ignorato.|  
  
 Se l'operatore nella proprietà del membro non è elencato nella tabella precedente, viene generato un errore. L'ordine di valutazione è determinato dall'ordine degli elementi di pari livello, non dalla precedenza degli operatori.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata una proprietà di membro denominata "Alternate Rollup Operator" contenente valori alternativi per gli operatori unari per eseguire il rollup degli elementi figlio della gerarchia Net Profit nella dimensione Account in un modo alternativo. Questa proprietà non esiste nel cubo Adventure Works, ma potrebbe essere creata. Questo utilizzo della funzione **RollupChildren** può essere utilizzato in un'applicazione di budget per l'analisi di simulazione.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
