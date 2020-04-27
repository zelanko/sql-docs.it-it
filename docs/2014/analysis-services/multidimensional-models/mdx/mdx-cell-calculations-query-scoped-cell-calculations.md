---
title: Creazione di calcoli di celle con ambito query (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 575bac6ba111259fe20540fd0b40f193f0a54b38
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074420"
---
# <a name="creating-query-scoped-cell-calculations-mdx"></a>Creazione di formule per il calcolo di celle con ambito query (MDX)
  Nel linguaggio MDX (Multidimensional Expressions) è possibile utilizzare la parola chiave `WITH` per descrivere celle calcolate nel contesto di una query. La parola chiave `WITH` ha la sintassi seguente:  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 Il valore `CellCalc_Identifier` contiene il nome delle celle calcolate. Il valore `String_Expression` contiene un elenco di espressioni set MDX ortogonali e unidimensionali. Ognuna di tali espressioni set deve essere risolta in una delle categorie elencate nella tabella seguente.  
  
|Category|Descrizione|  
|--------------|-----------------|  
|Set vuoto|Espressione set MDX che restituisce un set vuoto. In questo caso l'ambito della cella calcolata è costituito dall'intero cubo.|  
|Set con un singolo membro|Espressione set MDX che restituisce un singolo membro.|  
|Set di membri di un livello|Espressione set MDX che restituisce i membri di un singolo livello. Un esempio di tale espressione set è la *Level_Expression*.`Members` . Per includere i membri calcolati, utilizzare il *Level_Expression*.`AllMembers` . Per altre informazioni, vedere [AllMembers &#40;MDX&#41;](/sql/mdx/allmembers-mdx).|  
|Set di discendenti|Espressione set MDX che restituisce i discendenti di un membro specificato. Un esempio di tale espressione `Descendants`set è la funzione MDX (*Member_Expression*, *Level_Expresion* *Desc_Flag*). Per altre informazioni, vedere [Descendants &#40;MDX&#41;](/sql/mdx/descendants-mdx).|  
  
 Se l'argomento `String_Expression` non descrive una dimensione, MDX presupporrà che tutti i membri debbano essere inclusi al fine di costruire il sottocubo per il calcolo. Se l'argomento `String_Expression` è NULL, la definizione delle celle calcolate verrà pertanto applicata all'intero cubo.  
  
 L'argomento `MDX_Expression` contiene un'espressione MDX che restituisce un valore di cella per tutte le celle definite nell'argomento `String_Expression` .  
  
## <a name="additional-considerations"></a>Ulteriori considerazioni  
 In MDX la condizione di calcolo, specificata dalla proprietà `CONDITION`, viene elaborata una volta sola. Questa singola elaborazione consente di migliorare le prestazioni durante la valutazione di più definizioni di celle calcolate, soprattutto nel caso di celle calcolate sovrapposte nelle varie sessioni di calcolo del cubo.  
  
 Il momento in cui viene eseguita questa singola elaborazione dipende dall'ambito di creazione della definizione delle celle calcolate:  
  
-   Se la definizione viene creata con ambito globale, ovvero come parte di un cubo, la condizione di calcolo verrà elaborata insieme al cubo. Se viene apportata una modifica qualsiasi a celle del cubo incluse nel sottocubo di calcolo di una definizione di celle calcolate, la condizione di calcolo potrebbe non restituire risultati accurati fino a quando il cubo non verrà rielaborato. La modifica delle celle può essere dovuta, ad esempio, a operazioni di writeback. La condizione di calcolo viene rielaborata insieme al cubo.  
  
-   Se la definizione viene creata con ambito sessione, la condizione di calcolo verrà elaborata al momento dell'esecuzione dell'istruzione durante la sessione. Come nel caso delle definizioni di celle calcolate create a livello globale, se viene apportata una modifica alle celle la condizione di calcolo potrebbe non restituire risultati accurati per la definizione delle celle calcolate.  
  
-   Se la definizione viene creata con ambito query, la condizione di calcolo verrà elaborata all'esecuzione della query. Il problema legato alla modifica delle celle si presenta anche in questo caso, sebbene la latenza dei dati sia minima grazie al ridotto tempo di elaborazione per l'esecuzione delle query MDX.  
  
 La formula di calcolo, invece, viene elaborata ogni volta che sul cubo viene eseguita una query MDX che coinvolge celle incluse nella definizione delle celle calcolate, indipendentemente dall'ambito di creazione.  
  
## <a name="see-also"></a>Vedi anche  
 [Istruzione CREATE CELL CALCULATION &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-cell-calculation)  
  
  
