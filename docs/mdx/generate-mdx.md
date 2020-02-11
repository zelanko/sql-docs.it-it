---
title: Generate (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7a6008129d6b0a4c59412428c31f6e5de625f1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005902"
---
# <a name="generate-mdx"></a>Generate (MDX)


  Applica un set a ogni membro di un altro set e unisce i set risultanti tramite un join di unione. In alternativa, questa funzione restituisce una stringa concatenata creata valutando un'espressione stringa su un set.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Set_Expression1*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *Set_Expression2*  
 Espressione MDX (Multidimensional Expression) valida che restituisce un set.  
  
 *String_Expression*  
 Espressione stringa valida che corrisponde in genere al nome del membro corrente (CurrentMember.Name) di ogni tupla nel set specificato.  
  
 *Delimiter*  
 Delimitatore valido espresso come espressione stringa.  
  
## <a name="remarks"></a>Osservazioni  
 Se viene specificato un secondo set, la funzione **generate** restituisce un set generato applicando le tuple nel secondo set a ogni tupla del primo set, quindi unendo i set risultanti in base all'Unione. Se si specifica **All** , la funzione mantiene i duplicati nel set risultante.  
  
 Se viene specificata un'espressione stringa, la funzione **generate** restituisce una stringa generata dalla valutazione dell'espressione stringa specificata rispetto a ogni tupla nel primo set e quindi concatenando i risultati. Facoltativamente, è possibile delimitare la stringa separando i vari risultati nella stringa concatenata risultante.  
  
## <a name="examples"></a>Esempi  
  
### <a name="set"></a>Set  
 Nell'esempio seguente, la query restituisce un set che contiene la misura Internet Sales amount quattro volte, perché quattro sono i membri nel set [Date].[Calendar Year].[Calendar Year].MEMBERS:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 La rimozione di ALL modifica la query in modo che Internet Sales Amount sia restituito una sola volta:  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 L'uso pratico più comune di **generate** consiste nel valutare un'espressione set complessa, ad esempio il numero di riscontri, su un set di membri. Nell'esempio di query seguente vengono visualizzati i primi 10 prodotti per ogni anno di calendario su righe:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 Si noti che per ogni anno vengono visualizzati diversi primi 10 e che l'uso di **generate** è l'unico modo per ottenere questo risultato. Applicando un semplice crossjoin ai calendari e al set dei 10 prodotti migliori sarà possibile visualizzare i 10 migliori prodotti ogni volta, ripetuti per ogni anno, come illustrato nell'esempio seguente:  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>string  
 Nell'esempio seguente viene illustrato l'utilizzo di **generate** per restituire una stringa:  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  Questo formato della funzione **generate** può essere utile durante il debug dei calcoli, in quanto consente di restituire una stringa che Visualizza i nomi di tutti i membri di un set. Questo potrebbe essere più facile da leggere rispetto alla rigorosa rappresentazione MDX di un set restituito dalla funzione [SetToStr &#40;mdx&#41;](../mdx/settostr-mdx.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
