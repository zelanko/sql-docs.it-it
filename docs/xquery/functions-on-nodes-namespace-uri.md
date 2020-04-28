---
title: Funzione namespace-URI (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
ms.openlocfilehash: 05412c69aa121b9de14f2bab16555db2a8a4fdb4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67929947"
---
# <a name="functions-on-nodes---namespace-uri"></a>Funzioni su nodi - namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce l'URI dello spazio dei nomi del QName specificato in *$arg* come xs: String.  
  
## <a name="syntax"></a>Sintassi  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Nome del nodo di cui verrà recuperata la parte relativa all'URI dello spazio dei nomi.  
  
## <a name="remarks"></a>Osservazioni  
  
-   Se l'argomento viene omesso, l'impostazione predefinita è il nodo di contesto.  
  
-   In SQL Server, **FN: namespace-URI ()** senza un argomento può essere usato solo nel contesto di un predicato dipendente dal contesto. In particolare, può essere utilizzata solo tra parentesi ([ ]).  
  
-   Se *$arg* è la sequenza vuota, viene restituita la stringa di lunghezza zero.  
  
-   Se *$arg* è un nodo elemento o attributo il cui expanded-QName non è in uno spazio dei nomi, la funzione restituisce la stringa di lunghezza zero  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. Recupero dell'URI dello spazio dei nomi di un nodo specifico  
 La query seguente viene eseguita su un'istanza XML non tipizzata. L'espressione di query `namespace-uri(/ROOT[1])` recupera la parte relativa all'URI dello spazio dei nomi del nodo specificato.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Poiché l'elemento QName specificato non contiene l'URI dello spazio dei nomi, ma solo il nome locale, il risultato è una stringa di lunghezza zero.  
  
 La query seguente viene specificata sulla colonna **XML** instructions tipizzata. L'espressione `namespace-uri(/AWMI:root[1]/AWMI:Location[1])`restituisce l'URI dello spazio dei nomi del primo <`Location` elemento figlio> dell'elemento <`root`>.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Risultato:  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. Utilizzo di namespace-uri() senza argomento in un predicato  
 La query seguente viene specificata sulla colonna XML tipizzata CatalogDescription. L'espressione restituisce tutti i nodi elemento il cui URI dello spazio dei nomi è `https://www.adventure-works.com/schemas/OtherFeatures`. La funzione namespace-**URI ()** viene specificata senza un argomento e utilizza il nodo di contesto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Risultato parziale:  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 È possibile modificare l'URI dello spazio dei nomi nella query precedente in `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`. Si riceveranno quindi tutti gli elementi figlio del nodo elemento dell' `ProductDescription` <elemento> la cui parte URI dello spazio dei nomi `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`del QName espanso è.  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   La funzione **namespace-URI ()** restituisce istanze di tipo xs: String anziché XS: anyURI.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni sui nodi](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Funzione local-name &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
