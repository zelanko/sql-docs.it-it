---
title: Metodo exist() (tipo di dati xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f8b4c9b1526d34139723b505d724411f9fa48dc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765626"
---
# <a name="exist-method-xml-data-type"></a>Metodo exist() (tipo di dati xml)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce un **bit** che rappresenta una delle condizioni seguenti:  
  
-   1, che rappresenta True, se l'espressione XQuery di una query restituisce un risultato non vuoto, ovvero se restituisce almeno un nodo XML.  
  
-   0, che rappresenta False, se restituisce un risultato vuoto.  
  
-   NULL se l'istanza del tipo di dati **xml** sulla quale è stata eseguita la query contiene NULL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>Argomenti  
 XQuery  
 È un'espressione XQuery, un valore letterale stringa.  
  
## <a name="remarks"></a>Osservazioni  
  
> [!NOTE]  
>  Il metodo **exist()** restituisce 1 per l'espressione XQuery che restituisce un risultato non vuoto. Se si specifica la funzione **true()** o **false()** nel metodo **exist()** , il metodo **exist()** restituisce 1, in quanto le funzioni **true()** e **false()** restituiscono, rispettivamente, i valori booleani True e False, ovvero un risultato non vuoto. Il metodo **exist()** restituisce pertanto 1 (True), come illustrato nell'esempio seguente:  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come specificare il metodo **exist()** .  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>Esempio: specifica del metodo exist() su una variabile di tipo XML  
 Nell'esempio seguente, @x è una variabile di tipo **xml** (xml non tipizzato) e @f è una variabile di tipo Integer che archivia il valore restituito dal metodo **exist()** . Il metodo **exist()** restituisce (1) se il valore di data archiviato nell'istanza XML è `2002-01-01`.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 Nel confronto delle date nel metodo **exist()** si noti quanto segue:  
  
-   Il codice `cast as xs:date?` viene usato per il cast del valore al tipo **xs:date** ai fini del confronto.  
  
-   Il valore dell'attributo **\@Somedate** non è tipizzato. Nell'operazione di confronto, viene eseguito il cast implicito del valore al tipo sul lato destro del confronto, il tipo **xs:date**.  
  
-   Anziché **cast as xs:date()** è possibile usare la funzione costruttore **xs:date()** . Per altre informazioni, vedere [Constructor Functions &#40;XQuery&#41;](../../xquery/constructor-functions-xquery.md) (Funzioni costruttore &#40;XQuery&#41;).  
  
 L'esempio seguente è simile al precedente, ma contiene un elemento <`Somedate`>.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   Il metodo **text()** restituisce un nodo di testo che contiene il valore non tipizzato `2002-01-01`. (Il tipo dell'espressione XQuery è **xdt:untypedAtomic**.) È necessario eseguire il cast esplicito di questo valore tipizzato da **x** a **xsd:date**, poiché in questo caso il cast implicito non è supportato.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>Esempio: specifica del metodo exist() su una variabile XML tipizzata  
 Nell'esempio seguente viene illustrato l'uso del metodo **exist()** su una variabile di tipo **xml**. Si tratta di una variabile XML tipizzata, poiché specifica il nome della raccolta di spazi dei nomi dello schema, `ManuInstructionsSchemaCollection`.  
  
 Nell'esempio, un documento di istruzioni di produzione viene assegnato a questa variabile, quindi viene usato il metodo **exist()** per determinare se il documento include un elemento <`Location`> in cui il valore dell'attributo **LocationID** è 50.  
  
 Il metodo **exist()** specificato sulla variabile @x restituisce 1 (True) se il documento di istruzioni di produzione include un elemento <`Location`> con `LocationID=50`. In caso contrario, il metodo restituisce 0 (False).  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>Esempio: specifica del metodo exist() su una colonna di tipo XML  
 La query seguente recupera gli ID dei modelli di prodotto le cui descrizioni di catalogo non includono le specifiche, ovvero l'elemento <`Specifications`>:  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   La clausola WHERE seleziona solo le righe della tabella **ProductDescription** che soddisfano la condizione specificata sulla colonna di tipo **CatalogDescription xml**.  
  
-   Il metodo **exist()** della clausola WHERE restituisce 1 (True) se il codice XML non include elementi <`Specifications`>. Si noti l'uso della [funzione not() (XQuery)](../../xquery/functions-on-boolean-values-not-function.md).  
  
-   La [funzione sql:column() (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) viene usata per recuperare il valore da una colonna non XML.  
  
-   Questa query restituisce un set di righe vuoto.  
  
 La query specifica i metodi **query()** e **exist()** del tipo di dati xml ed entrambi i metodi dichiarano gli stessi spazi dei nomi nel prologo della query. In questo caso è possibile utilizzare WITH XMLNAMESPACES per dichiarare il prefisso e utilizzarlo nella query.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere spazi dei nomi alle query con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Confronto dati XML tipizzati con dati XML non tipizzati](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Creare istanze di dati XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [metodi con tipo di dati XML](../../t-sql/xml/xml-data-type-methods.md)   
 [Linguaggio XML di manipolazione dei dati &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
