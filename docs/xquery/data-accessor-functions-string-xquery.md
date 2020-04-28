---
title: Funzione String (XQuery) | Microsoft Docs
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
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cb30d81102c17f2c3ce04b31ac7ff2b9689343e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038938"
---
# <a name="data-accessor-functions---string-xquery"></a>Funzioni di accesso dati - string (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il valore di *$arg* rappresentato come stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 È un nodo o un valore atomico.  
  
## <a name="remarks"></a>Osservazioni  
  
-   Se *$arg* è la sequenza vuota, viene restituita la stringa di lunghezza zero.  
  
-   Se *$arg* è un nodo, la funzione restituisce il valore stringa del nodo ottenuto tramite la funzione di accesso stringa-valore. definita nella specifica W3C "XQuery 1.0 and XPath 2.0 Data Model".  
  
-   Se *$arg* è un valore atomico, la funzione restituisce la stessa stringa restituita dal cast dell'espressione come **xs: String**, *$arg*, tranne quando specificato diversamente.  
  
-   Se il tipo di *$arg* è **xs: anyURI**, l'URI viene convertito in una stringa senza caratteri di escape per i caratteri speciali.  
  
-   In questa implementazione, **FN: String ()** senza un argomento può essere usato solo nel contesto di un predicato dipendente dal contesto. In particolare, può essere utilizzata solo tra parentesi ([ ]).  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
### <a name="a-using-the-string-function"></a>A. Utilizzo della funzione string  
 La query seguente recupera la <`Features`> nodo elemento figlio dell'elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Risultato parziale:  
  
```  
<PD:Features xmlns:PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 Se si specifica la funzione **String ()** , si riceverà il valore stringa del nodo specificato.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Di seguito è riportato il risultato parziale.  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. Utilizzo della funzione string su vari nodi  
 Nell'esempio seguente, un'istanza XML viene assegnata a una variabile di tipo XML. Le query vengono specificate per illustrare il risultato dell'applicazione di **String ()** a vari nodi.  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 La query seguente recupera il valore stringa del nodo del documento. Il valore è formato dalla concatenazione del valore stringa di tutti i relativi nodi di testo discendenti.  
  
```  
select @x.query('string(/)')  
```  
  
 Risultato:  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 La query seguente tenta il recupero del valore stringa del nodo di un'istruzione di elaborazione. Il risultato è una sequenza vuota, poiché non contiene un nodo di testo.  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 La query seguente recupera il valore stringa del nodo di commento e restituisce il nodo di testo.  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 Risultato:  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
