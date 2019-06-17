---
title: Funzione data (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ac37c6d3a55be4f11a4ad925a950724d5d791d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62934836"
---
# <a name="data-accessor-functions---data-xquery"></a>Funzioni di accesso dati - data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il valore tipizzato per ciascun elemento specificato da *$arg*.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di elementi per i quali verranno restituiti i valori tipizzati.  
  
## <a name="remarks"></a>Note  
 Per i valori tipizzati sono valide le osservazioni seguenti:  
  
-   Il valore tipizzato di un valore atomico è il valore atomico.  
  
-   Il valore tipizzato di un nodo di testo è il valore stringa del nodo di testo.  
  
-   Il valore tipizzato di un commento è il valore stringa del commento.  
  
-   Il valore tipizzato di un'istruzione di elaborazione è il contenuto dell'istruzione, senza il relativo nome di destinazione.  
  
-   Il valore tipizzato di un nodo documento è il relativo valore stringa.  
  
 Per i nodi attributo ed elemento sono valide le osservazioni seguenti:  
  
-   Se un nodo attributo è tipizzato con un tipo di XML Schema, il relativo valore tipizzato è il valore tipizzato corrispondente.  
  
-   Se il nodo dell'attributo è tipizzato, il relativo valore tipizzato è uguale al valore stringa che viene restituito come un'istanza di **xdt: untypedAtomic**.  
  
-   Se il nodo dell'elemento non è stato tipizzato, il relativo valore tipizzato è uguale al valore stringa che viene restituito come un'istanza di **xdt: untypedAtomic**.  
  
 Per i nodi elemento tipizzati sono valide le osservazioni seguenti:  
  
-   Se l'elemento ha un tipo di contenuto semplice **data ()** restituisce il valore tipizzato dell'elemento.  
  
-   Se il nodo è di tipo complesso, xs: anyType, compresi **data ()** restituisce un errore statico.  
  
 Anche se tramite il **data ()** funzione è spesso facoltativa, come illustrato negli esempi seguenti, specificando la **data ()** funzione aumenta in modo esplicito la leggibilità della query. Per altre informazioni, vedere [nozioni fondamentali su XQuery](../xquery/xquery-basics.md).  
  
 Non è possibile specificare **data ()** nel codice XML creato, come illustrato nell'esempio seguente:  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. Utilizzo della funzione XQuery data() per estrarre il valore tipizzato di un nodo  
 La query seguente viene illustrato come la **data ()** funzione viene utilizzata per recuperare i valori di attributo, un elemento e un nodo di testo:  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Questo è il risultato:  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 Come accennato, il **data ()** funzione è facoltativa durante la creazione di attributi. Se non si specifica la **data ()** funzione, in modo implicito presuppone. La query seguente genera gli stessi risultati della query precedente:  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Gli esempi seguenti illustrano le istanze in cui il **data ()** è necessaria la funzione.  
  
 Nella query seguente, **$pd / pD/P1:Specifications/Material / materiale** restituisce il <`Material`> elemento. È inoltre **dei dati ($pd/pD/P1:Specifications/Material/materiale)** restituisce dati di tipo carattere tipizzati come xdt: untypedAtomic, perché <`Material`> non è tipizzato. Quando l'input è non tipizzato, il risultato del **data ()** tipizzata come **xdt: untypedAtomic**.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Questo è il risultato:  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 Nella query seguente, **data($pd/p1:Features/wm:Warranty)** restituisce un errore statico perché <`Warranty`> è un elemento di tipo complesso.  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
