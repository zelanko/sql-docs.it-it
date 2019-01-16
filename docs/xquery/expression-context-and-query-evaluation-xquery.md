---
title: Contesto delle espressioni e valutazione delle Query (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f8092182bff23580936e17923985739525309097
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256876"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>Contesto delle espressioni e valutazione delle query (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Il contesto di un'espressione è rappresentato dalle informazioni che ne consentono l'analisi e la valutazione. Di seguito sono illustrate le due fasi della valutazione di XQuery:  
  
-   **Contesto statico** -questa è la fase di compilazione di query. A seconda delle informazioni disponibili, durante l'analisi statica della query a volte vengono generati errori.  
  
-   **Contesto dinamico** -questa è la fase di esecuzione di query. Anche se in una query non si verificano errori statici, ad esempio durante la compilazione, è possibile che vengano generati errori durante l'esecuzione della query.  
  
## <a name="static-context"></a>Contesto statico  
 L'inizializzazione del contesto statico prevede la raccolta di tutte le informazioni necessarie per l'analisi statica dell'espressione. Nella fase di inizializzazione vengono eseguite le operazioni seguenti:  
  
-   Il **spazi vuoti limite** criterio è impostato su striscia. Di conseguenza, gli spazi vuoti limite non viene mantenuto per la **qualsiasi elemento** e **attributo** costruttori nella query. Ad esempio:  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     Questa query restituisce il risultato seguente, perché lo spazio limite viene escluso durante l'analisi dell'espressione XQuery:  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   Il prefisso e l'associazione allo spazio dei nomi vengono inizializzati per gli elementi seguenti:  
  
    -   Un set di spazi dei nomi predefiniti.  
  
    -   Gli spazi dei nomi definiti utilizzando WITH XMLNAMESPACES. Per altre informazioni, vedere [aggiungere gli spazi dei nomi alle query con WITH XMLNAMESPACES](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)).  
  
    -   Gli spazi dei nomi definiti nel prologo della query. Si noti che le dichiarazioni degli spazi dei nomi nel prologo possono avere la priorità sulla dichiarazione dello spazio dei nomi di WITH XMLNAMESPACES. Nella query seguente, ad esempio, WITH XMLNAMESPACES viene dichiarato un prefisso (pd) che lo associa allo spazio dei nomi (`https://someURI`). Nella clausola WHERE, tuttavia, il prologo della query ha la priorità su tale associazione.  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     Tutte le associazioni di spazi dei nomi vengono risolte durante l'inizializzazione del contesto statico.  
  
-   Se una query su un oggetto tipizzato **xml** colonna o una variabile, i componenti della raccolta di XML schema associata alla colonna o variabile vengono importati nel contesto statico. Per altre informazioni, vedere [Confrontare dati XML tipizzati con dati XML non tipizzati](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
-   Per ogni tipo atomico presente negli schemi importati, nel contesto statico viene inoltre resa disponibile una funzione di cast, come illustrato nell'esempio seguente. In questo esempio viene specificata una query su un oggetto tipizzato **xml** variabile. La raccolta di XML Schema associata alla variabile definisce un tipo atomico, myType. Corrispondente a questo tipo, una funzione di cast **myType()**, è disponibile durante l'analisi statica. L'espressione della query (`ns:myType(0)`) restituisce un valore di tipo myType.  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     Nell'esempio seguente, la funzione cast per la **int** tipo XML predefinito viene specificato nell'espressione.  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 Dopo che il contesto statico è stato inizializzato, viene analizzata (compilata) l'espressione della query. L'analisi statica include le operazioni seguenti:  
  
1.  Analisi della query.  
  
2.  Risoluzione dei nomi della funzione e del tipo specificati nell'espressione.  
  
3.  Tipizzazione statica della query, che consente di verificare che la query sia indipendente dai tipi. Ad esempio, la query seguente restituisce un errore statico perché il **+** operatore richiede argomenti di tipo primitive numerico:  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     Nell'esempio seguente, il **Value ()** operatore richiede un singleton. Come specificato nel XML schema, possono esserci più \<Elem > elementi. L'analisi statica dell'espressione determina che non è indipendente dai tipi e viene restituito un errore statico. Per risolvere l'errore, è necessario riformulare l'espressione in modo da specificare in modo esplicito un singleton (`data(/x:Elem)[1]`).  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     Per altre informazioni, vedere [XQuery e tipizzazione statica](../xquery/xquery-and-static-typing.md).  
  
### <a name="implementation-restrictions"></a>Limitazioni di implementazione  
 Di seguito sono elencate le limitazioni correlate al contesto statico:  
  
-   La modalità di compatibilità XPath non è supportata.  
  
-   Per la costruzione del codice XML, è supportata solo la modalità di costruzione con rimozione. Si tratta dell'impostazione predefinita. Pertanto, il tipo di nodo elemento costruito è della **xdt: non tipizzato** tipo e gli attributi sono dello **xdt: untypedAtomic** tipo.  
  
-   È supportata solo la modalità ordinata.  
  
-   Sono supportati solo i criteri di rimozione dello spazio XML.  
  
-   La funzionalità URI di base non è supportata.  
  
-   **fn:doc()** non è supportato.  
  
-   **fn:Collection()** non è supportato.  
  
-   Il flagger statico XQuery non è disponibile.  
  
-   Le regole di confronto associate le **xml** viene usato il tipo di dati. Vengono sempre impostate le regole di confronto dei punti di codice Unicode.  
  
## <a name="dynamic-context"></a>Contesto dinamico  
 Il contesto dinamico indica le informazioni che devono essere disponibili durante l'esecuzione dell'espressione. Oltre al contesto statico, le informazioni seguenti vengono inizializzate come parte del contesto dinamico:  
  
-   L'elemento di contesto, la posizione del contesto e le dimensioni del contesto vengono inizializzate come illustrato di seguito. Si noti che tutti questi valori possono eseguire l'override di [metodo Nodes ()](../t-sql/xml/nodes-method-xml-data-type.md).  
  
    -   Il **xml** tipo di dati imposta l'elemento di contesto, il nodo da elaborare, al nodo del documento.  
  
    -   La posizione del contesto, ovvero la posizione dell'elemento di contesto rispetto ai nodi da elaborare, viene innanzitutto impostata su 1.  
  
    -   Le dimensioni del contesto, ovvero il numero di elementi della sequenza da elaborare, vengono innanzitutto impostate su 1, perché esiste sempre un nodo del documento.  
  
### <a name="implementation-restrictions"></a>Limitazioni di implementazione  
 Di seguito sono elencate le limitazioni correlate al contesto dinamico:  
  
-   Il **data e ora correnti** funzioni di contesto **fn:current-data**, **fn:current-tempo**, e **fn:current-dateTime**, non sono è supportato.  
  
-   Il **fuso orario implicito** è fissa UTC+0 e non può essere modificato.  
  
-   Il **fn:doc()** funzione non è supportata. Tutte le query vengono eseguite **xml** variabili o colonne di tipo.  
  
-   Il **fn:collection()** funzione non è supportata.  
  
## <a name="see-also"></a>Vedere anche  
 [XQuery Basics](../xquery/xquery-basics.md)   
 [Confronto dati XML tipizzati con dati XML non tipizzati](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Raccolte di XML Schema &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
