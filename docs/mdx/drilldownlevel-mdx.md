---
description: DrilldownLevel (MDX)
title: DrilldownLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3bd1f2214820a1795ae8d279c88a0d86c2ca5843
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194013"
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)


  Esegue il drill-down dei membri di un set al livello inferiore al livello più basso rappresentato nel set.  
  
 La specifica del livello in cui eseguire il drill-down è facoltativa, ma se si imposta il livello è possibile utilizzare un' **espressione di livello** o un livello di **Indice**. Questi argomenti si escludono a vicenda. Infine, se i membri calcolati sono presenti nella query, è possibile specificare un argomento per includerli nel set di righe.  
  
## <a name="syntax"></a>Sintassi  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Level_Expression*  
 (Facoltativo) Espressione MDX che identifica in modo esplicito il livello in cui eseguire il drill-down. Se si specifica un'espressione di livello, ignorare l'argomento index seguente.  
  
 *Index*  
 (Facoltativo) Espressione numerica valida che specifica il numero della gerarchia in cui eseguire il drill-down all'interno di un set. È possibile usare il livello di indice anziché Level_Expression per identificare in modo esplicito il livello in cui eseguire il drill-down.  
  
 *Include_Calc_Members*  
 (Facoltativo) Flag che indica se includere i membri calcolati, se presenti, al livello di drill-down.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **DrilldownLevel** restituisce un set di membri figlio in ordine gerarchico in base ai membri inclusi nel set specificato. L'ordine originale dei membri nel set specificato viene mantenuto, con la sola differenza che nel set di risultati della funzione tutti i membri figlio vengono indicati immediatamente sotto il membro padre corrispondente.  
  
 Con una struttura dati gerarchica multilivello è possibile scegliere in modo esplicito un livello in cui eseguire il drill-down. Per specificare il livello sono disponibili due modalità che si escludono a vicenda. Il primo approccio consiste nell'impostare l'argomento **Level_Expression** usando un'espressione MDX che restituisce il livello, un approccio alternativo consiste nel specificare l'argomento **index** , usando un'espressione numerica che specifica il livello per numero.  
  
 Se si specifica un'espressione di livello, la funzione restituisce un set in ordine gerarchico recuperando solo i figli dei membri del livello specificato. Se si specifica un'espressione di livello ma nessun membro è presente in tale livello, l'espressione di livello viene ignorata.  
  
 Se si specifica un valore di indice, la funzione restituisce un set in ordine gerarchico recuperando solo i figli dei membri del livello inferiore successivo della gerarchia indicata nel set specificato, secondo un indice in base zero.  
  
 Se non si specifica un'espressione di livello né un valore di indice, la funzione restituisce un set in ordine gerarchico recuperando solo i figli dei membri del livello inferiore della prima dimensione indicata nel set specificato.  
  
 Eseguendo una query sulla proprietà XMLA MdpropMdxDrillFunctions è possibile verificare il livello di supporto fornito dal server per le funzioni di drill-through. per informazioni dettagliate, vedere [Proprietà XMLA supportate &#40;&#41;XMLA ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
## <a name="examples"></a>Esempi  
 È possibile provare gli esempi seguenti nella finestra Query MDX in SSMS, usando il cubo Adventure Works.  
  
 **Esempio 1: illustra la sintassi minima**  
  
 Nel primo esempio viene illustrata la sintassi minima per **DrilldownLevel**. L'unico argomento richiesto è un'espressione set. Si noti che quando si esegue questa query, si ottiene il padre [tutte le categorie] e i membri del livello successivo verso il basso: [Accessories], [Bikes] e così via. Sebbene questo esempio sia semplice, viene illustrato lo scopo di base della funzione **DrilldownLevel** , che consente di eseguire il drill-down fino al livello successivo.  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Esempio 2: sintassi alternativa usando un livello di indice esplicito  
  
 Questo esempio illustra la sintassi alternativa, in cui il livello di indice viene specificato tramite un'espressione numerica. In questo caso, il livello di indice è 0. Per un indice in base zero, si tratta del livello più basso.  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 Si noti che il set di risultati è identico alla query precedente. Come regola generale, non è necessario impostare il livello di indice a meno che non si voglia avviare il drill-down in un livello specifico. Rieseguire la query precedente, impostando il valore di indice su 1, quindi su 2. Con un valore di indice impostato su 1, il drill-down viene avviato nel secondo livello della gerarchica. Con un valore di indice impostato su 2, il drill-down viene avviato nel terzo livello, il livello più alto in questo esempio. Più elevato è il numero, più alto è il livello di indice.  
  
 **Esempio 3: illustra un'espressione di livello**  
  
 L'esempio successivo mostra come usare un'espressione di livello. Con un set che rappresenta una struttura gerarchica, l'uso di un'espressione di livello consente di scegliere un livello nella gerarchia in cui avviare il drill-down.  
  
 In questo esempio, il livello di drill-down inizia da [City] come secondo argomento della funzione **DrilldownLevel** . Quando si esegue questa query, il drill-down viene avviato nel livello [City], per gli stati Washington e Oregon. Per la funzione **DrilldownLevel** , il set di risultati include anche i membri al livello successivo, [Postal Cap].  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **Esempio 4-inclusione di membri calcolati**  
  
 Nell'ultimo esempio viene illustrato un membro calcolato, che viene visualizzato nella parte inferiore del set di risultati quando si aggiunge il flag di **include_calculated_members** . Si noti che il flag viene specificato come quarto parametro.  
  
 Questo esempio funziona perché il membro calcolato è allo stesso livello dei membri non calcolati. Il membro calcolato [West Coast] è composto dai membri di [United States], più tutti i membri del livello inferiore a [United States].  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 Se si rimuove solo il flag e si riesegue la query, si ottengono gli stessi risultati meno il membro calcolato [West Coast].  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
