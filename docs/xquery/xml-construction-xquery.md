---
title: Costruzione di strutture XML (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 51c1898ddaee1ecf878944a3b43c3d8adbb38590
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946174"
---
# <a name="xml-construction-xquery"></a>Costruzione di strutture XML (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In XQuery, è possibile usare la **diretto** e **calcolata** costruttori per la costruzione di strutture XML all'interno di una query.  
  
> [!NOTE]  
>  Non c'è alcuna differenza tra il **diretto** e **calcolata** costruttori.  
  
## <a name="using-direct-constructors"></a>Utilizzo dei costruttori diretti  
 Quando si utilizzano i costruttori diretti, nella costruzione delle strutture XML si specifica una sintassi in stile XML. Negli esempi seguenti viene illustrata la costruzione delle strutture XML mediante i costruttori diretti.  
  
### <a name="constructing-elements"></a>Costruzione di elementi  
 Con le annotazioni XML è possibile costruire elementi. Nell'esempio seguente usa l'espressione del costruttore diretto di elementi e crea un \<ProductModel > elemento. L'elemento costruito dispone di tre elementi figlio  
  
-   Un nodo di testo.  
  
-   Due nodi elemento, \<Summary > e \<funzionalità >.  
  
    -   Il \<Summary > elemento ha un nodo di testo figlio il cui valore è "Some description".  
  
    -   Il \<funzionalità > elemento dispone di tre nodi elemento figlio, \<colore >, \<peso >, e \<Warranty >. Ognuno di questi nodi ha un nodo di testo figlio. I valori dei nodi sono rispettivamente "Red", "25" e "2 years parts and labor".  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 Codice XML risultante:  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 Anche se la costruzione di elementi da espressioni costanti, come illustrato in questo esempio, può risultare utile, il punto forte di questa caratteristica del linguaggio XQuery è costituito dalla possibilità di costruire strutture XML che estraggono i dati da un database in modo dinamico. È possibile utilizzare le parentesi graffe per specificare le espressioni di query. Nel codice XML risultante l'espressione viene sostituita dal relativo valore. Ad esempio, la query seguente crea un <`NewRoot`> elemento con un elemento figlio (<`e`>). Il valore dell'elemento <`e`> viene calcolato specificando un'espressione di percorso fra parentesi graffe ("{...}").  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 La parentesi fungono da token di cambio del contesto e attivano il passaggio dalla modalità di costruzione di strutture XML alla modalità di valutazione della query. In questo caso viene valutata l'espressione di percorso XQuery all'interno delle parentesi, `/root` e al suo posto vengono inseriti i relativi risultati.  
  
 Questo è il risultato:  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 La query successiva è simile alla precedente. Tuttavia, l'espressione fra parentesi graffe specifica la **data ()** funzione per recuperare il valore atomico del <`root`> elemento e lo assegna all'elemento costruito, <`e`>.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 Questo è il risultato:  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 Se si desidera utilizzare le parentesi graffe come parte del testo invece che come token di scambio del contesto, è necessario utilizzare la relativa sequenza di escape "}}" o "{{", come illustrato in questo esempio:  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 Questo è il risultato:  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 La query seguente è un altro esempio di creazione di elementi mediante il costruttore diretto di elementi. Inoltre, il valore della <`FirstLocation`> elemento viene ottenuto eseguendo l'espressione fra parentesi graffe. L'espressione della query restituisce le fasi di produzione nel primo centro di lavorazione dalla colonna Instructions della tabella Production.ProductModel.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Questo è il risultato:  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>Contenuto dell'elemento nella costruzione di strutture XML  
 Nell'esempio seguente viene illustrato il funzionamento delle espressioni nella creazione del contenuto dell'elemento utilizzando il costruttore diretto di elementi. Nell'esempio seguente, il costruttore diretto di elementi specifica un'espressione. In base a questa espressione, nel codice XML risultante viene creato un nodo di testo.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 La sequenza di valori atomici risultante dalla valutazione dell'espressione viene aggiunta al nodo di testo con l'aggiunta di uno spazio fra i valori atomici adiacenti, come illustrato nel risultato. L'elemento creato ha un figlio, un nodo di testo contenente il valore mostrato nel risultato.  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 Se anziché una sola espressione si specificano tre espressioni separate che generano tre nodi di testo, nel codice XML risultante i nodi di testo adiacenti vengono uniti in un singolo nodo di testo, per concatenazione.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 Il nodo di elemento creato ha un figlio, un nodo di testo contenente il valore mostrato nel risultato.  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>Costruzione di attributi  
 Quando si costruiscono elementi utilizzando il costruttore diretto di elementi è possibile specificarne gli attributi utilizzando sintassi in stile XML, come illustrato nell'esempio seguente:  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 Codice XML risultante:  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 L'elemento costruito <`ProductModel`> ha un attributo ProductModelID e i nodi figlio:  
  
-   Un nodo di testo, `This is product model catalog description.`  
  
-   Un nodo elemento, <`Summary`>. Questo nodo ha un nodo di testo figlio, `Some description`.  
  
 Quando si costruisce un attributo è possibile specificarne il valore mediante un'espressione fra parentesi graffe. In questo caso, il valore dell'espressione viene restituito come valore dell'attributo.  
  
 Nell'esempio seguente, il **data ()** funzione non è strettamente necessaria. Poiché si sta assegnando il valore dell'espressione a un attributo **data ()** viene applicata in modo implicito per recuperare il valore tipizzato dell'espressione specificata.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 Questo è il risultato:  
  
```xml
<NewRoot attr="5" />  
```  
  
 Di seguito viene riportato un altro esempio nel quale vengono specificate espressioni per la costruzione degli attributi LocationID e SetupHrs. Le espressioni vengono valutate in base al codice XML nella colonna Instruction. Il valore tipizzato dell'espressione viene assegnato agli attributi.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 Risultato parziale:  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step ...   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Le espressioni di attributo multiple o miste (stringa ed espressione XQuery) non sono supportate. Ad esempio, come illustrato nella query seguente, si costruisce una struttura XML dove `Item` è una costante e il valore `5` viene ottenuto valutando un'espressione di query:  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     La query seguente restituisce un errore, perché combina una stringa costante con un'espressione ({/x}) e ciò non è supportato:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     In questo caso sono disponibili le opzioni seguenti:  
  
    -   Formare il valore dell'attributo mediante la concatenazione di due valori atomici. Tali valori atomici vengono serializzati nel valore dell'attributo con uno spazio fra un valore e l'altro:  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         Questo è il risultato:  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   Usare la [Concat-funzione](../xquery/functions-on-string-values-concat.md) per concatenare i due argomenti stringa in valore di attributo risultante:  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         In questo caso, fra i due valori stringa non vengono aggiunti spazi. Se si desidera l'aggiunta di uno spazio fra i valori è necessario inserirlo esplicitamente.  
  
         Questo è il risultato:  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   Le espressioni multiple come valore di attributo non sono supportate. Ad esempio, la query seguente restituisce un errore:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   Le sequenze eterogenee non sono supportate. Qualsiasi tentativo di assegnare una sequenza eterogenea come valore di attributo provocherà la restituzione di un errore, come illustrato nell'esempio seguente. In questo esempio, una sequenza eterogenea, una stringa "Item" e un elemento <`x`>, viene specificato come valore dell'attributo:  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     Se si applica il **data ()** funzione, la query funziona, poiché recupera il valore atomico dell'espressione, `/x`, che è concatenato la stringa. Quella che segue è una sequenza di valori atomici:  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     Questo è il risultato:  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   L'ordine del nodo attributo viene applicato durante la serializzazione anziché durante il controllo dei tipi statici. Ad esempio, la query seguente ha esito negativo poiché tenta di aggiungere un attributo dopo un nodo non attributo.  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     La query precedente restituisce l'errore seguente:  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>Aggiunta degli spazi dei nomi  
 Quando si costruiscono strutture XML utilizzando i costruttori diretti, è possibile qualificare i nomi degli elementi e degli attributi costruiti mediante un prefisso di spazio dei nomi. È possibile associare il prefisso allo spazio dei nomi come indicato di seguito:  
  
-   Utilizzando un attributo di dichiarazione dello spazio dei nomi.  
  
-   Utilizzando la clausola WITH XMLNAMESPACES.  
  
-   Nel prologo della XQuery.  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>Utilizzo di un attributo di dichiarazione dello spazio dei nomi per l'aggiunta degli spazi dei nomi  
 L'esempio seguente usa un attributo di dichiarazione dello spazio dei nomi nella costruzione dell'elemento <`a`> per dichiarare uno spazio dei nomi predefinito. La costruzione dell'elemento figlio <`b`> Annulla la dichiarazione dello spazio dei nomi predefinito dichiarato nell'elemento padre.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 Questo è il risultato:  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 È possibile assegnare allo spazio dei nomi un prefisso, Specificandolo nella costruzione dell'elemento <`a`>.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 Questo è il risultato:  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 È possibile annullare la dichiarazione di uno spazio dei nomi predefinito nella costruzione di strutture XML, ma non di un prefisso di spazio dei nomi. La query seguente restituisce un errore, perché non è possibile annullare la-dichiara un prefisso come specificato nella costruzione dell'elemento <`b`>.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 Il nuovo spazio dei nomi costruito è disponibile per l'utilizzo all'interno della query. Ad esempio, la query seguente dichiara uno spazio dei nomi nella costruzione dell'elemento <`FirstLocation`> e specifica il prefisso nelle espressioni per i valori degli attributi LocationID e SetupHrs.  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Si noti che un nuovo prefisso di spazio dei nomi creato in questo modo sostituirà le dichiarazioni dello spazio dei nomi preesistenti per il prefisso. Ad esempio, la dichiarazione dello spazio dei nomi, `AWMI="https://someURI"`, nella query prologo è sottoposto a override dalla dichiarazione dello spazio dei nomi di <`FirstLocation`> elemento.  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="https://someURI";  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>Utilizzo di un prologo per l'aggiunta degli spazi dei nomi  
 In questo esempio viene illustrata l'aggiunta degli spazi dei nomi alla struttura XML costruita. Nel prologo della query viene dichiarato uno spazio dei nomi predefinito.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 Si noti che nella costruzione dell'elemento <`b`>, l'attributo di dichiarazione dello spazio dei nomi è specificato con una stringa vuota come relativo valore. In questo modo la dichiarazione dello spazio dei nomi predefinito dichiarato nel padre viene annullata.  
  

Questo è il risultato:  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>Costruzione di strutture XML e gestione degli spazi vuoti  
 Il contenuto dell'elemento nella costruzione di strutture XML può includere spazi vuoti. Tali spazi vengono gestiti come descritto di seguito:  
  
-   I caratteri spazi vuoti nello spazio dei nomi URI vengono considerati come il tipo XSD **anyURI**. Nello specifico:  
  
    -   Gli spazi vuoti iniziali e finali vengono rimossi.  
  
    -   Gli spazi vuoti all'interno delle istruzioni vengono compressi in un unico spazio  
  
-   I caratteri di avanzamento riga all'interno del contenuto dell'attributo vengono sostituiti con spazi. Tutti gli altri spazi vuoti restano invariati.  
  
-   Lo spazio vuoto all'interno degli elementi viene mantenuto.  
  
 Nell'esempio seguente viene illustrata la gestione degli spazi vuoti nella costruzione di strutture XML:  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   https://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 Questo è il risultato:  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>Altri costruttori XML diretti  
 I costruttori per le istruzioni di elaborazione e i commenti XML utilizzano la stessa sintassi del costrutto XML corrispondente. Sono inoltre supportati costruttori calcolati per i nodi di testo, ma vengono utilizzati principalmente nel linguaggio XML DML per la costruzione di nodi di testo.  
  
 **Nota** per un esempio dell'uso di un costruttore di nodi di testo esplicito, vedere l'esempio specifico in [insert &#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md).  
  
 Nella query seguente il costrutto XML include un elemento, due attributi, un commento e un'istruzione di elaborazione. Si noti che viene usata una virgola prima di <`FirstLocation`>, perché viene generata una sequenza.  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 Risultato parziale:  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>Utilizzo dei costruttori calcolati  
 . In questo caso si specificano le parole chiave che identificano il tipo di nodo da costruire. Sono supportate solo le parole chiave seguenti:  
  
-   element  
  
-   attributo  
  
-   text  
  
 Per i nodi elemento e attributo, le parole chiave sono seguite dal nome del nodo e dall'espressione, racchiusa fra parentesi, che genera il contenuto del nodo. Nell'esempio seguente si costruisce il codice XML successivo:  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 Di seguito è riportata la query che utilizza i costruttori calcolati per generare il codice XML:  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 L'espressione che genera il contenuto del nodo può specificare un'espressione di query.  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 Si noti che i costruttori di nodi e attributi calcolati, come definiti nella specifica XQuery, consentono il calcolo dei nomi dei nodi. Quando si utilizzano i costruttori diretti in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è necessario specificare i nomi dei nodi, ad esempio elemento e attributo, come valori letterali costanti. Non esistono pertanto differenze fra costruttori di elementi e attributi diretti e calcolati.  
  
 Nell'esempio seguente, il contenuto dei nodi costruiti viene ottenuto da istruzioni di produzione XML archiviate nella colonna Instructions della **xml** tipo di dati della tabella ProductModel.  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 Risultato parziale:  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>Ulteriori limitazioni di implementazione  
 I costruttori di attributi calcolati non possono essere utilizzati per dichiarare un nuovo spazio dei nomi. I seguenti costruttori calcolati non sono inoltre supportati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Costruttori di nodi di documento calcolati  
  
-   Costruttori di istruzioni di elaborazione calcolate  
  
-   Costruttori di commenti calcolati  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni XQuery](../xquery/xquery-expressions.md)  
  
  
