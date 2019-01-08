---
title: La corrispondenza dei tipi di sequenza | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence type matching [XQuery]
- XQuery, sequence type matching
ms.assetid: 8c56fb69-ca04-4aba-b55a-64ae216c492d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3df2ef3f14cb8ca4fd7e7bcf5799b6966c16dc10
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511451"
---
# <a name="type-system---sequence-type-matching"></a>Sistema di tipi - Corrispondenza per il tipo di sequenza
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Il valore di un'espressione XQuery è sempre rappresentato da una sequenza di zero o più elementi, che possono essere valori atomici o nodi. Il tipo di sequenza fa riferimento alla capacità di stabilire una corrispondenza tra il tipo di sequenza restituito da un'espressione di query e un tipo specifico. Ad esempio:  
  
-   Se il valore dell'espressione è atomico, è possibile stabilire se è di tipo integer, decimal o string.  
  
-   Se il valore dell'espressione è un nodo XML, è possibile stabilire se è un nodo di commento, un nodo istruzione di elaborazione o un nodo di testo.  
  
-   È possibile stabilire se l'espressione restituisce un elemento XML o un nodo di attributo con un nome e un tipo specifico.  
  
 Per individuare una corrispondenza per il tipo di sequenza, è possibile utilizzare l'operatore booleano `instance of`. Per altre informazioni sul `instance of` espressione, vedere [espressioni SequenceType &#40;XQuery&#41;](../xquery/sequencetype-expressions-xquery.md).  
  
## <a name="comparing-the-atomic-value-type-returned-by-an-expression"></a>Confronto del tipo del valore atomico restituito da un'espressione  
 Se un'espressione restituisce una sequenza di valori atomici, potrebbe essere necessario trovare il tipo del valore nella sequenza. Negli esempi seguenti viene illustrato l'utilizzo della sintassi del tipo di sequenza per valutare il tipo di valore atomico restituito da un'espressione.  
  
### <a name="example-determining-whether-a-sequence-is-empty"></a>Esempio: Determinare se una sequenza è vuota  
 Il **della Empty ()** tipo di sequenza utilizzabile in un'espressione sequencetype per determinare se la sequenza restituita dall'espressione specificata è una sequenza vuota.  
  
 Nell'esempio seguente, l'XML Schema consente che l'elemento <`root`> supporti i valori Null:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 Se un'istanza XML tipizzata specifica un valore per l'elemento <`root`>, `instance of empty()` restituisce False.  
  
```  
DECLARE @var XML(SC1)  
SET @var = '<root>1</root>'  
-- The following returns False  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
 Se l'elemento <`root`> supporta i valori Null nell'istanza, il relativo valore è una sequenza vuota e `instance of empty()` restituisce True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" />'  
SELECT @var.query('data(/root[1]) instance of  empty() ')  
GO  
```  
  
### <a name="example-determining-the-type-of-an-attribute-value"></a>Esempio: Determinazione del tipo di un valore di attributo  
 A volte è possibile valutare il tipo di sequenza restituito da un'espressione prima dell'elaborazione. Ad esempio, si consideri uno XML Schema nel quale un nodo è definito come un tipo unione. Nell'esempio seguente, l'XML Schema della raccolta definisce l'attributo `a` come un tipo unione il cui valore può essere di tipo decimal o string.  
  
```  
-- Drop schema collection if it exists.  
-- DROP XML SCHEMA COLLECTION SC.  
-- GO  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
  <element name="root">  
    <complexType>  
       <sequence/>  
         <attribute name="a">  
            <simpleType>  
               <union memberTypes="decimal string"/>  
            </simpleType>  
         </attribute>  
     </complexType>  
  </element>  
</schema>'  
GO  
```  
  
 Prima di elaborare un'istanza XML tipizzata, è possibile determinare il tipo del valore dell'attributo `a`. Nell'esempio seguente, il valore dell'attributo `a` è di tipo decimal e pertanto `, instance of xs:decimal` restituisce True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="2.5"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:decimal')  
GO  
```  
  
 L'attributo `a` viene modificato in un tipo string e pertanto `instance of xs:string` restituirà True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root a="Hello"/>'  
SELECT @var.query('data((/root/@a)[1]) instance of xs:string')  
GO  
```  
  
### <a name="example-cardinality-in-sequence-expressions"></a>Esempio: Cardinalità nelle espressioni di sequenza  
 Nell'esempio seguente viene illustrato l'effetto della cardinalità in un'espressione di sequenza. L'XML Schema seguente definisce un elemento <`root`> che è di tipo byte e supporta i valori Null.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema">  
      <element name="root" nillable="true" type="byte"/>  
</schema>'  
GO  
```  
  
 Nella query seguente, dato che l'espressione restituisce un singleton di tipo byte, `instance of` restituisce True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root>111</root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
```  
  
 Se si imposta l'elemento <`root`> come Null, il relativo valore è una sequenza vuota. ovvero l'espressione `/root[1]` restituisce una sequenza vuota e pertanto `instance of xs:byte` restituisce False. Si noti che in questo caso la cardinalità predefinita è 1.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte ')   
GO  
-- result = false  
```  
  
 Se si specifica la cardinalità aggiungendo l'indicatore di occorrenza (`?`), l'espressione della sequenza restituisce True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xsi:nil="true" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"></root>'  
SELECT @var.query('data(/root[1]) instance of  xs:byte? ')   
GO  
-- result = true  
```  
  
 Si noti che il test di un'espressione SequenceType include due fasi:  
  
1.  Il test determina innanzitutto se il tipo di espressione corrisponde al tipo specificato.  
  
2.  In caso affermativo, il test determina se il numero di elementi restituiti dall'espressione corrisponde all'indicatore di occorrenza specificato.  
  
 Se entrambe le condizioni sono vere, l'espressione `instance of` restituisce True.  
  
### <a name="example-querying-against-an-xml-type-column"></a>Esempio: L'esecuzione di query su una colonna di tipo xml  
 Nell'esempio seguente, una query viene eseguita su una colonna Instructions della **xml** digitare il [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] database. Si tratta di una colonna XML tipizzata, perché è associata a uno schema. Tramite XML Schema viene definito l'attributo `LocationID` di tipo integer. Pertanto, nell'espressione di sequenza, il `instance of xs:integer?` restituisce True.  
  
```  
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
data(/AWMI:root[1]/AWMI:Location[1]/@LocationID) instance of xs:integer?') as Result   
FROM Production.ProductModel   
WHERE ProductModelID = 7  
```  
  
## <a name="comparing-the-node-type-returned-by-an-expression"></a>Confronto del tipo di nodo restituito da un'espressione  
 Se un'espressione restituisce una sequenza di nodi, è possibile che sia necessario individuare il tipo di nodo nella sequenza. Nell'esempio seguente viene illustrata la sintassi del tipo che è possibile utilizzare per valutare il tipo di nodo restituito da un'espressione. È possibile utilizzare i tipi di sequenza seguenti:  
  
-   **Item ()** -corrisponde a qualsiasi elemento nella sequenza.  
  
-   **Node ()** -determina se la sequenza è un nodo.  
  
-   **//Processing-Instruction ()** -determina se l'espressione restituisce un'istruzione di elaborazione.  
  
-   **comment** -determina se l'espressione restituisce un commento.  
  
-   **document-node()** -determina se l'espressione restituisce un nodo di documento.  
  
 Nell'esempio seguente vengono illustrati questi tipi di sequenza.  
  
### <a name="example-using-sequence-types"></a>Esempio: Utilizzo di tipi di sequenza  
 In questo esempio vengono eseguite numerose query su una variabile XML non tipizzata. Le query illustrano l'utilizzo dei tipi di sequenza.  
  
```  
DECLARE @var XML  
SET @var = '<?xml-stylesheet href="someValue" type="text/xsl" ?>  
<root>text node  
  <!-- comment 1 -->   
  <a>Data a</a>  
  <!-- comment  2 -->  
</root>'  
```  
  
 Nella prima query, l'espressione restituisce il valore tipizzato dell'elemento <`a`>. Nella seconda query, l'espressione restituisce l'elemento <`a`>. In entrambi i casi si tratta di elementi e pertanto entrambe le query restituiscono True.  
  
```  
SELECT @var.query('data(/root[1]/a[1]) instance of item()')  
SELECT @var.query('/root[1]/a[1] instance of item()')  
```  
  
 Tutte le espressioni XQuery nelle tre query seguenti restituiscono il nodo figlio dell'elemento <`root`>. L'espressione SequenceType `instance of node()` restituisce pertanto True e le altre due espressioni, `instance of text()` e `instance of document-node()`, restituiscono False.  
  
```  
SELECT @var.query('(/root/*)[1] instance of node()')  
SELECT @var.query('(/root/*)[1] instance of text()')  
SELECT @var.query('(/root/*)[1] instance of document-node()')   
```  
  
 Nella query seguente, l'espressione `instance of document-node()` restituisce True perché il padre dell'elemento <`root`> è un nodo di documento.  
  
```  
SELECT @var.query('(/root/..)[1] instance of document-node()') -- true  
```  
  
 Nella query seguente, l'espressione recupera il primo nodo dall'istanza XML. Poiché è un nodo istruzione di elaborazione, l'espressione `instance of processing-instruction()` restituisce True.  
  
```  
SELECT @var.query('(/node())[1] instance of processing-instruction()')  
```  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Sono valide le limitazioni seguenti:  
  
-   **document-node()** con tipo di contenuto non è supportata la sintassi.  
  
-   **Processing-Instruction(Name)** sintassi non è supportata.  
  
## <a name="element-tests"></a>Test dell'elemento  
 Un test dell'elemento consente di stabilire una corrispondenza tra il nodo elemento restituito da un'espressione e un nodo elemento con un nome e un tipo specifico. Sono disponibili i test dell'elemento seguenti:  
  
```  
element ()  
element(ElementName)  
element(ElementName, ElementType?)   
element(*, ElementType?)  
```  
  
## <a name="attribute-tests"></a>Test dell'attributo  
 Il test dell'attributo consente di stabilire se l'attributo restituito da un'espressione è un nodo di attributo. Sono disponibili i test dell'attributo seguenti:  
  
 `attribute()`  
  
 `attribute(AttributeName)`  
  
 `attribute(AttributeName, AttributeType)`  
  
## <a name="test-examples"></a>Esempi di test  
 Negli esempi seguenti vengono illustrati scenari nei quali i test dell'elemento e dell'attributo possono risultare utili.  
  
### <a name="example-a"></a>Esempio A  
 L'XML Schema seguente definisce il tipo complesso `CustomerType` nel quale gli elementi <`firstName`> e <`lastName`> sono facoltativi. Per un'istanza XML specificata, potrebbe essere necessario stabilire se esiste il nome di un cliente specifico.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
targetNamespace="myNS" xmlns:ns="myNS">  
  <complexType name="CustomerType">  
     <sequence>  
        <element name="firstName" type="string" minOccurs="0"   
                  nillable="true" />  
        <element name="lastName" type="string" minOccurs="0"/>  
     </sequence>  
  </complexType>  
  <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS">  
<firstName>SomeFirstName</firstName>  
<lastName>SomeLastName</lastName>  
</x:customer>'  
```  
  
 La query seguente utilizza un'espressione `instance of element (firstName)` per determinare se il primo elemento figlio di <`customer`> è un elemento denominato <`firstName`>. In caso affermativo, restituisce True.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
     (/x:customer/*)[1] instance of element (firstName)')  
GO  
```  
  
 Se si rimuove l'elemento <`firstName`> dall'istanza, la query restituirà False.  
  
 È inoltre possibile utilizzare:  
  
-   La sintassi del tipo di sequenza `element(ElementName, ElementType?)`, come illustrato nella query seguente. Tale sintassi stabilisce una corrispondenza per un nodo elemento denominato `firstName` e di tipo `xs:string` che supporta o non supporta i valori Null.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS";   
    (/x:customer/*)[1] instance of element (firstName, xs:string?)')  
    ```  
  
-   La sintassi del tipo di sequenza `element(*, type?)`, come illustrato nella query seguente. Tale sintassi stabilisce una corrispondenza per il nodo elemento se è di tipo `xs:string`, indipendentemente dal nome.  
  
    ```  
    SELECT @var.query('declare namespace x="myNS"; (/x:customer/*)[1] instance of element (*, xs:string?)')  
    GO  
    ```  
  
### <a name="example-b"></a>Esempio B  
 Nell'esempio seguente viene illustrato come determinare se il nodo restituito da un'espressione è un nodo elemento con un nome specifico, Usa il **Element ()** di test.  
  
 Nell'esempio seguente, i due elementi <`Customer`> dell'istanza XML sui quali viene eseguita la query sono di due tipi diversi, `CustomerType` e `SpecialCustomerType`. Si supponga di voler conoscere il tipo dell'elemento <`Customer`> restituito dall'espressione. La raccolta di XML Schema seguente definisce i tipi `CustomerType` e `SpecialCustomerType`.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
          targetNamespace="myNS"  xmlns:ns="myNS">  
  <complexType name="CustomerType">  
    <sequence>  
      <element name="firstName" type="string"/>  
      <element name="lastName" type="string"/>  
    </sequence>  
  </complexType>  
  <complexType name="SpecialCustomerType">  
     <complexContent>  
       <extension base="ns:CustomerType">  
        <sequence>  
            <element name="Age" type="int"/>  
        </sequence>  
       </extension>  
     </complexContent>  
    </complexType>  
   <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 Questa raccolta di XML schema consente di creare un oggetto tipizzato **xml** variabile. L'istanza XML assegnata alla variabile include due elementi <`customer`> di tipo diverso. Il primo elemento è di tipo `CustomerType` e il secondo elemento è di tipo `SpecialCustomerType`.  
  
```  
DECLARE @var XML(SC)  
SET @var = '  
<x:customer xmlns:x="myNS">  
   <firstName>FirstName1</firstName>  
   <lastName>LastName1</lastName>  
</x:customer>  
<x:customer xsi:type="x:SpecialCustomerType" xmlns:x="myNS" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">  
   <firstName> FirstName2</firstName>  
   <lastName> LastName2</lastName>  
   <Age>21</Age>  
</x:customer>'  
```  
  
 Nella query seguente, l'espressione `instance of element (*, x:SpecialCustomerType ?)` restituisce False, perché restituisce il primo elemento Customer che non è di tipo `SpecialCustomerType`.  
  
```  
SELECT @var.query('declare namespace x="myNS";   
    (/x:customer)[1] instance of element (*, x:SpecialCustomerType ?)')  
```  
  
 Se si modifica l'espressione della query precedente e si recupera il secondo elemento <`customer`> (`/x:customer)[2]`), `instance of` restituirà True.  
  
### <a name="example-c"></a>Esempio C  
 In questo esempio viene utilizzato il test dell'attributo. L'XML Schema seguente definisce il tipo complesso CustomerType con gli attributi CustomerID e Age. L'attributo Age è facoltativo. È possibile determinare se nell'elemento <`customer`> di un'istanza XML specifica è presente l'attributo Age.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="https://www.w3.org/2001/XMLSchema"  
       targetNamespace="myNS" xmlns:ns="myNS">  
<complexType name="CustomerType">  
  <sequence>  
     <element name="firstName" type="string" minOccurs="0"   
               nillable="true" />  
     <element name="lastName" type="string" minOccurs="0"/>  
  </sequence>  
  <attribute name="CustomerID" type="integer" use="required" />  
  <attribute name="Age" type="integer" use="optional" />  
 </complexType>  
 <element name="customer" type="ns:CustomerType"/>  
</schema>  
'  
GO  
```  
  
 La query seguente restituisce True perché nell'istanza XML su cui viene eseguita la query esiste un nodo di attributo al quale è assegnato il nome `Age`. In questa espressione viene utilizzato il test dell'attributo `attribute(Age)`. Gli attributi non sono ordinati, pertanto la query utilizza l'espressione FLWOR per recuperare tutti gli attributi per poi testare ognuno di essi tramite l'espressione `instance of`. Nell'esempio viene creata una raccolta di XML schema per creare un oggetto tipizzato **xml** variabile.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<x:customer xmlns:x="myNS" CustomerID="1" Age="22" >  
<firstName>SomeFName</firstName>  
<lastName>SomeLName</lastName>  
</x:customer>'  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age)) THEN  
        "true"  
        ELSE  
        ()')     
GO  
  
```  
  
 Se si rimuove dall'istanza l'attributo facoltativo `Age`, la query precedente restituirà False.  
  
 Nel test dell'attributo è possibile specificare il nome e il tipo dell'attributo (`attribute(name,type)`).  
  
```  
SELECT @var.query('declare namespace x="myNS";   
FOR $i in /x:customer/@*  
RETURN  
    IF ($i instance of attribute (Age, xs:integer)) THEN  
        "true"  
        ELSE  
        ()')  
```  
  
 In alternativa, è possibile specificare il `attribute(*, type)` sintassi del tipo di sequenza. Se il tipo di attributo corrisponde al tipo specificato, in questo modo viene stabilita una corrispondenza per il nodo di attributo, indipendentemente dal nome.  
  
### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Sono valide le limitazioni seguenti:  
  
-   Nel test dell'elemento, il nome del tipo deve essere seguito dall'indicatore di occorrenza (**?**).  
  
-   **Element (ElementName, TypeName)** non è supportato.  
  
-   **elemento (\*, TypeName)** non è supportato.  
  
-   **schema-Element()** non è supportato.  
  
-   **schema-Attribute(AttributeName)** non è supportato.  
  
-   In modo esplicito l'esecuzione di query per **xsi: Type** oppure **xsi: nil** non è supportato.  
  
## <a name="see-also"></a>Vedere anche  
 [Sistema di tipi &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
