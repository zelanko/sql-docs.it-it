---
title: CoalesceEmpty (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f760220b02396591e684a83305111e487908d19b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006300"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


  Converte un valore di cella vuota in un valore di cella non vuota specificato, che può corrispondere a un numero o una stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Numeric_Expression1*  
 Espressione numerica valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce un numero.  
  
 *Numeric_Expression2*  
 Espressione numerica valida che in genere è un valore numerico specificato.  
  
 *String_Expression1*  
 Espressione stringa valida che in genere è un'espressione MDX (Multidimensional Expression) di coordinate di celle che restituisce una stringa.  
  
 *String_Expression2*  
 Espressione stringa valida che in genere è un valore stringa specificato con cui viene sostituito un valore NULL restituito dalla prima espressione stringa.  
  
## <a name="remarks"></a>Osservazioni  
 Se vengono specificate una o più espressioni numeriche, la funzione **CoalesceEmpty** restituisce il valore numerico della prima espressione numerica, da sinistra a destra, che può essere risolta in un valore non vuoto. Se nessuna delle espressioni numeriche specificate può essere risolta in un valore non vuoto, la funzione restituisce il valore di cella vuota. Il valore della seconda espressione numerica è in genere il valore numerico con cui viene sostituito un valore NULL restituito dalla prima espressione numerica.  
  
 Se vengono specificate una o più espressioni stringa, la funzione restituisce il valore stringa della prima espressione stringa, da sinistra a destra, che può essere risolta in un valore non vuoto. Se nessuna delle espressioni stringa specificate può essere risolta in un valore non vuoto, la funzione restituisce il valore di cella vuota. Il valore della seconda espressione stringa è in genere il valore stringa con cui viene sostituito un valore NULL restituito dalla prima espressione stringa.  
  
 La funzione **CoalesceEmpty** può assumere solo valori dello stesso tipo. In altre parole, tutte le espressioni valore specificate devono restituire solo tipi di dati numerici o un valore di cella vuota oppure tutte le espressioni valore specificate devono restituire tipi di dati stringa o un valore di cella vuota. Nella stessa chiamata a questa funzione non possono essere incluse espressioni numeriche e stringa.  
  
 Per ulteriori informazioni sulle celle vuote, vedere la documentazione relativa a OLE DB.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene eseguita una query sul cubo **Adventure Works** . Nell'esempio viene restituito il quantitativo ordinato di ogni prodotto e la percentuale di quantitativi ordinati per categoria. La funzione **CoalesceEmpty** garantisce che i valori null siano rappresentati come zero (0) durante la formattazione dei membri calcolati.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](../mdx/mdx-function-reference-mdx.md)  
  
  
