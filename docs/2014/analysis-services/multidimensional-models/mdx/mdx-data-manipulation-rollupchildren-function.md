---
title: Utilizzo della funzione RollupChildren (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 325d932a0c14cf4ca6b4ecf9e2349fb8064c45bd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699766"
---
# <a name="working-with-the-rollupchildren-function-mdx"></a>Utilizzo della funzione RollupChildren (MDX)
  Espressioni MDX (MDX) [RollupChildren](/sql/mdx/rollupchildren-mdx) (funzione) [Script per la ricerca e sostituzione] esegue il rollup di elementi figlio di un membro, applicando un operatore unario diverso a ogni elemento figlio e restituisce il valore di tale rollup sotto forma di numero. L'operatore unario utilizzato può essere specificato da una proprietà del membro associata al membro figlio oppure può essere costituito da un'espressione stringa fornita direttamente alla funzione.  
  
## <a name="rollupchildren-function-examples"></a>Esempi sulla funzione RollupChildren  
 L'utilizzo della funzione `RollupChildren` nelle istruzioni MDX (Multidimensional Expressions) è semplice da spiegare, ma questa funzione può avere un'ampia gamma di effetti sulle query MDX.  
  
 L'effetto della funzione `RollupChildren` viene rilevato nelle query MDX progettate per l'esecuzione dell'analisi selettiva sui dati esistenti di un cubo. Nella tabella seguente è ad esempio riportato un elenco di membri figlio per il membro padre Net Sales, con i relativi operatori unari (rappresentati dalla proprietà `UNARY_OPERATOR` del membro) indicati tra parentesi.  
  
|Membro padre|Membro figlio|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 Il membro padre Net Sales specifica le vendite nette totali meno i valori delle vendite nazionali ed estere lorde, sottraendo i resi nazionali ed esteri durante il rollup.  
  
 Si desidera tuttavia fornire una previsione semplice e rapida delle vendite lorde nazionali ed estere maggiorata del 10%, ignorando i resi nazionali ed esteri. Per calcolare tale valore, è possibile utilizzare la funzione `RollupChildren` in uno dei due modi seguenti: con una proprietà personalizzata del membro o con la funzione `IIf`.  
  
### <a name="using-a-custom-member-property"></a>Utilizzo di una proprietà personalizzata del membro  
 Se il calcolo del rollup deve essere eseguito di frequente, è consigliabile creare una proprietà di membro in cui memorizzare l'operatore da utilizzare per ogni membro figlio per una funzione specifica. Nella tabella seguente sono indicati gli operatori unari validi e vengono descritti i risultati previsti.  
  
|Operatore|Risultato|  
|--------------|------------|  
|+|totale = totale + membro figlio corrente|  
|-|totale = totale - membro figlio corrente|  
|*|totale = totale * membro figlio corrente|  
|/|totale = totale / membro figlio corrente|  
|~|Il membro figlio non viene utilizzato nel rollup e il suo valore viene ignorato.|  
  
 È ad esempio possibile creare una proprietà di membro denominata `SALES_OPERATOR` alla quale possono essere assegnati gli operatori unari indicati nella tabella seguente.  
  
|Membro padre|Membro figlio|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 Con questa nuova proprietà di membro, l'istruzione MDX seguente esegue l'operazione di stima delle vendite lorde in modo rapido ed efficace, ignorando i resi nazionali ed esteri:  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 Quando la funzione viene chiamata, il valore di ogni membro figlio viene applicato a un totale utilizzando l'operatore archiviato nella proprietà del membro. I membri relativi ai resi nazionali ed esteri vengono ignorati e il totale di rollup restituito dalla funzione `RollupChildren` viene moltiplicato per 1,1.  
  
### <a name="using-the-iif-function"></a>Utilizzo della funzione IIf  
 Se l'operazione di esempio non è comune oppure se l'operazione si applica solo a una query MDX, il [IIf](/sql/mdx/iif-mdx) funzione può essere utilizzata con la `RollupChildren` funzione per fornire lo stesso risultato. La query MDX seguente genera lo stesso risultato dell'esempio precedente, ma senza ricorrere a una proprietà di membro personalizzata:  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 L'istruzione MDX esamina l'operatore unario del membro figlio. Se l'operatore unario viene utilizzato per eseguire una sottrazione, ad esempio quando sono presenti resi nazionali ed esteri, la funzione `IIf` sostituisce l'operatore unario ~, in caso contrario la funzione `IIf` utilizza l'operatore unario del membro figlio. Il totale di rollup restituito viene infine moltiplicato per 1,1 per determinare il valore della stima per le vendite nazionali ed estere lorde.  
  
## <a name="see-also"></a>Vedere anche  
 [Manipolazione dei dati &#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  
