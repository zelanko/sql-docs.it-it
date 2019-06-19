---
title: 'Specifica profondità nelle relazioni ricorsive mediante SQL: max-depth | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- max-depth annotation
- XPath queries [SQLXML], recursive relationships
- depth in recursive relationships [SQLXML]
- annotated XSD schemas, recursive relationships
- relationships [SQLXML], recursive relationships
- self joins
- recursive relationships [SQLXML]
- recursion [SQLXML]
- sql:max-depth
- recursive joins [SQLXML]
ms.assetid: 0ffdd57d-dc30-44d9-a8a0-f21cadedb327
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b247efb895f037965620c7430a3dc41c33fe550
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013654"
---
# <a name="specifying-depth-in-recursive-relationships-by-using-sqlmax-depth"></a>Specifica del livello di nidificazione nelle relazioni ricorsive mediante sql:max-depth
  Quando nei database relazionali una tabella viene coinvolta in una relazione con sé stessa, si parla di relazione ricorsiva. In una relazione supervisore-supervisionato (supervisor-supervisee), ad esempio, una tabella in cui sono archiviati i record dei dipendenti è coinvolta in una relazione con sé stessa. In questo caso, la stessa tabella dei dipendenti ricopre il ruolo di supervisore da un lato della relazione e di supervisionato dall'altro lato.  
  
 Gli schemi di mapping possono includere relazioni ricorsive nelle quali un elemento e il rispettivo predecessore sono dello stesso tipo.  
  
## <a name="example-a"></a>Esempio A  
 Si consideri la tabella seguente:  
  
```  
Emp (EmployeeID, FirstName, LastName, ReportsTo)  
```  
  
 Nella colonna ReportsTo di questa tabella viene archiviato l'ID dipendente del responsabile.  
  
 Si supponga di voler generare una gerarchia XML di dipendenti nella quale il dipendente responsabile si trova al primo posto e i dipendenti che sono sotto la supervisione del responsabile vengono visualizzati nella gerarchia corrispondente, come mostrato nel frammento XML di esempio seguente. Novità in questo frammento viene mostrato il *struttura ad albero ricorsiva* per il dipendente 1.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
     <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
     <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
        <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
          <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
...  
...  
</root>  
```  
  
 In questo frammento il dipendente 5 è sotto la supervisione del dipendente 4, il dipendente 4 è sotto la supervisione del dipendente 3 e i dipendenti 3 e 2 sono sotto la supervisione del dipendente 1.  
  
 Per produrre questo risultato, è possibile utilizzare lo schema XSD seguente e specificare una query XPath in tale schema. Lo schema descrive un'  **\<Emp >** elemento di tipo EmployeeType, costituito da un  **\<Emp >** elemento figlio dello stesso tipo, EmployeeType. Si tratta di una relazione ricorsiva (l'elemento e il rispettivo predecessore sono dello stesso tipo). Inoltre, lo schema Usa un'  **\<SQL: Relationship >** per descrivere la relazione padre-figlio tra il supervisore e supervisionato. Si noti che in questo  **\<SQL: Relationship >** , Emp rappresenta sia l'elemento padre che la tabella figlio.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="6" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Dal momento che la relazione è ricorsiva, è necessario trovare un modo per specificare il livello di nidificazione della ricorsione nello schema. In caso contrario, il risultato sarà una ricorsione infinita (il dipendente che è sotto la supervisione del dipendente che, a sua volta è sotto la supervisione del dipendente e così via). L'annotazione `sql:max-depth` consente di specificare il livello di nidificazione da raggiungere nella ricorsione. In questo particolare esempio, per specificare un valore per `sql:max-depth`, è necessario conoscere il livello di nidificazione della gerarchia di gestione nella società.  
  
> [!NOTE]  
>  Lo schema specifica l'annotazione `sql:limit-field` ma non specifica l'annotazione `sql:limit-value`. Questa situazione limita il nodo principale nella gerarchia risultante ai soli dipendenti che non sono sottoposti ad alcuna supervisione (ReportsTo è NULL). Che specifica `sql:limit-field` e se non si specifica `sql:limit-value` (che per impostazione predefinita su NULL) dell'annotazione esegue questa operazione. Se si desidera che l'XML risultante includa ogni possibile albero gerarchico (l'albero gerarchico per ogni dipendente della tabella), rimuovere l'annotazione `sql:limit-field` dallo schema.  
  
> [!NOTE]  
>  Nella procedura riportata di seguito viene utilizzato il database tempdb.  
  
#### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Creare una tabella di esempio chiamata Emp nel database tempdb al quale punta la radice virtuale.  
  
    ```  
    USE tempdb  
    CREATE TABLE Emp (  
           EmployeeID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Emp values (1, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Emp values (2, 'Andrew', 'Fuller',1)  
    INSERT INTO Emp values (3, 'Janet', 'Leverling',1)  
    INSERT INTO Emp values (4, 'Margaret', 'Peacock',3)  
    INSERT INTO Emp values (5, 'Steven', 'Devolio',4)  
    INSERT INTO Emp values (6, 'Nancy', 'Buchanan',5)  
    INSERT INTO Emp values (7, 'Michael', 'Suyama',6)  
    ```  
  
3.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome maxDepth.xml.  
  
4.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file con il nome maxDepthT.xml nella stessa directory nella quale è stato salvato maxDepth.xml. La query nel modello restituisce tutti i dipendenti della tabella Emp.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="maxDepth.xml">  
        /Emp  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (maxDepth.xml) è relativo alla directory nella quale viene salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\maxDepth.xml"  
    ```  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello. Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Questo è il risultato:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2" LastName="Fuller" />   
    <Emp FirstName="Janet" EmployeeID="3" LastName="Leverling">  
      <Emp FirstName="Margaret" EmployeeID="4" LastName="Peacock">  
        <Emp FirstName="Steven" EmployeeID="5" LastName="Devolio">  
          <Emp FirstName="Nancy" EmployeeID="6" LastName="Buchanan">  
            <Emp FirstName="Michael" EmployeeID="7" LastName="Suyama" />   
          </Emp>  
        </Emp>  
      </Emp>  
    </Emp>  
  </Emp>  
</root>  
```  
  
> [!NOTE]  
>  Per produrre livelli di nidificazione di gerarchie diverse nel risultato, modificare il valore dell'annotazione `sql:max-depth` nello schema ed eseguire nuovamente il modello dopo ogni modifica.  
  
 Nello schema precedente, tutte le  **\<Emp >** elementi presentavano esattamente lo stesso set di attributi (**EmployeeID**, **FirstName**, e  **LastName**). Nello schema seguente è stato lievemente modificato per restituire un'ulteriore **ReportsTo** attributo per tutti i  **\<Emp >** gli elementi che fanno riferimento a una gestione.  
  
 Questo frammento XML, ad esempio, mostra i subalterni del dipendente 1:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
<Emp FirstName="Nancy" EmployeeID="1" LastName="Devolio">  
  <Emp FirstName="Andrew" EmployeeID="2"   
       ReportsTo="1" LastName="Fuller" />   
  <Emp FirstName="Janet" EmployeeID="3"   
       ReportsTo="1" LastName="Leverling">  
...  
...  
```  
  
 Questo è lo schema corretto:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:documentation>  
      Customer-Order-Order Details Schema  
      Copyright 2000 Microsoft. All rights reserved.  
    </xsd:documentation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"  
                  parent-key="EmployeeID"  
                  child="Emp"  
                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
                   type="EmpType"   
                   sql:relation="Emp"   
                   sql:key-fields="EmployeeID"   
                   sql:limit-field="ReportsTo" />  
  <xsd:complexType name="EmpType">  
    <xsd:sequence>  
       <xsd:element name="Emp"   
                    type="EmpType"   
                    sql:relation="Emp"   
                    sql:key-fields="EmployeeID"  
                    sql:relationship="SupervisorSupervisee"  
                    sql:max-depth="6"/>  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:int" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
    <xsd:attribute name="ReportsTo" type="xsd:int" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
## <a name="sqlmax-depth-annotation"></a>Annotazione sql:max-depth  
 In un schema costituito da relazioni ricorsive il livello di nidificazione della ricorsione deve essere specificata in modo esplicito. Questa operazione è necessaria per produrre correttamente la query FOR XML EXPLICIT corrispondente che restituisce i risultati richiesti.  
  
 Utilizzare l'annotazione `sql:max-depth` nello schema per specificare il livello di nidificazione della ricorsione in una relazione ricorsiva descritta nello schema. Il valore della `sql:max-depth` annotazione è un numero intero positivo (da 1 a 50) che indica il numero di ricorsioni:  Un valore pari a 1 arresta la ricorsione in corrispondenza dell'elemento per cui il `sql:max-depth` annotazione è specificata; un valore pari a 2 Arresta la ricorsione al livello successivo dall'elemento in corrispondenza del quale `sql:max-depth` è specificato; e così via.  
  
> [!NOTE]  
>  Nell'implementazione sottostante una query XPath specificata rispetto a uno schema di mapping viene convertita in un'istruzione SELECT... PER la query XML EXPLICIT. Questa query richiede che venga specificato un livello di nidificazione limitato della ricorsione. Più alto è il valore specificato per `sql:max-depth`, più grande sarà la query FOR XML EXPLICIT che verrà generata, con un probabile rallentamento del tempo di recupero.  
  
> [!NOTE]  
>  Gli updategram e il caricamento bulk XML ignorano l'annotazione max-depth, pertanto gli inserimenti o gli aggiornamenti ricorsivi si verificheranno indipendentemente dal valore specificato per max-depth.  
  
## <a name="specifying-sqlmax-depth-on-complex-elements"></a>Specifica di sql:max-depth per gli elementi complessi  
 L'annotazione `sql:max-depth` può essere specificata su qualsiasi elemento di contenuto complesso.  
  
### <a name="recursive-elements"></a>Elementi ricorsivi  
 Se viene specificato un valore `sql:max-depth` sia per l'elemento padre che per l'elemento figlio in una relazione ricorsiva, l'annotazione `sql:max-depth` specificata per l'elemento padre ha la precedenza. Nello schema seguente, ad esempio, l'annotazione `sql:max-depth` viene specificata per gli elementi dipendente sia padre che figlio. In questo caso `sql:max-depth=4`specificato per il  **\<Emp >** elemento padre (che ricopre il ruolo di supervisore), ha la precedenza. Il `sql:max-depth` specificato nell'elemento figlio  **\<Emp >** elemento (che ricopre il ruolo di supervisionato) viene ignorato.  
  
#### <a name="example-b"></a>Esempio B  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"  
                                  parent="Emp"  
                                  parent-key="EmployeeID"  
                                  child="Emp"  
                                  child-key="ReportsTo" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp" type="EmployeeType"   
                          sql:relation="Emp"   
                          sql:key-fields="EmployeeID"   
                          sql:limit-field="ReportsTo"   
                          sql:max-depth="3" />  
  <xsd:complexType name="EmployeeType">  
    <xsd:sequence>  
      <xsd:element name="Emp" type="EmployeeType"   
                              sql:relation="Emp"   
                              sql:key-fields="EmployeeID"  
                              sql:relationship="SupervisorSupervisee"  
                              sql:max-depth="2" />  
    </xsd:sequence>   
    <xsd:attribute name="EmployeeID" type="xsd:ID" />  
    <xsd:attribute name="FirstName" type="xsd:string"/>  
    <xsd:attribute name="LastName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Per testare questo schema, seguire i passaggi forniti per il precedente esempio A in questo argomento.  
  
### <a name="nonrecursive-elements"></a>Elementi non ricorsivi  
 Se l'annotazione `sql:max-depth` viene specificata per un elemento dello schema che non determina una ricorsione, viene ignorata. Nello schema seguente, un'  **\<Emp >** elemento costituito da una  **\<costante >** elemento figlio, che, a sua volta, presenta un  **\<Emp >** elemento figlio.  
  
 In questo schema, il `sql:max-depth` annotazione specificata per il  **\<costante >** elemento viene ignorato perché non è nessuna ricorsione tra il  **\<Emp >** padre e il  **\<costante >** elemento figlio. Ma non esiste ricorsione tra il  **\<Emp >** predecessore e il  **\<Emp >** figlio. Lo schema specifica l'annotazione `sql:max-depth` per entrambi. Pertanto, il `sql:max-depth` annotazione specificata per il predecessore ( **\<Emp >** ricopre il ruolo di supervisore) ha la precedenza.  
  
#### <a name="example-c"></a>Esempio C  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="SupervisorSupervisee"   
                  parent="Emp"   
                  child="Emp"   
                  parent-key="EmployeeID"   
                  child-key="ReportsTo"/>  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="Emp"   
               sql:relation="Emp"   
               type="EmpType"  
               sql:limit-field="ReportsTo"  
               sql:max-depth="1" />  
    <xsd:complexType name="EmpType" >  
      <xsd:sequence>  
       <xsd:element name="Constant"   
                    sql:is-constant="1"   
                    sql:max-depth="20" >  
         <xsd:complexType >  
           <xsd:sequence>  
            <xsd:element name="Emp"   
                         sql:relation="Emp" type="EmpType"  
                         sql:relationship="SupervisorSupervisee"   
                         sql:max-depth="3" />  
         </xsd:sequence>  
         </xsd:complexType>  
         </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="EmployeeID" type="xsd:int" />  
    </xsd:complexType>  
</xsd:schema>  
```  
  
 Per testare questo schema, seguire i passaggi forniti per il precedente esempio A in questo argomento.  
  
## <a name="complex-types-derived-by-restriction"></a>Tipi complessi derivati dalla restrizione  
 Se si dispone di una derivazione da di tipo complesso  **\<restrizione >** , gli elementi del corrispondente tipo complesso di base non è possibile specificare il `sql:max-depth` annotazione. In questi casi, l'annotazione `sql:max-depth` può essere aggiunta all'elemento del tipo derivato.  
  
 D'altra parte, se si dispone di una derivazione da di tipo complesso  **\<estensione >** , gli elementi del tipo complesso base corrispondente possono specificare la `sql:max-depth` annotazione.  
  
 Lo schema XSD seguente, ad esempio, genera un errore in quanto l'annotazione `sql:max-depth` viene specificata per il tipo di base. Questa annotazione non è supportata su un tipo derivato da  **\<restrizione >** da un altro tipo. Per correggere questo problema, è necessario modificare lo schema e specificare l'annotazione `sql:max-depth` per l'elemento nel tipo derivato.  
  
#### <a name="example-d"></a>Esempio D  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:dt="urn:schemas-microsoft-com:datatypes"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:complexType name="CustomerBaseType">   
    <xsd:sequence>  
       <xsd:element name="CID" msdata:field="CustomerID" />  
       <xsd:element name="CompanyName"/>  
       <xsd:element name="Customers" msdata:max-depth="3">  
         <xsd:annotation>  
           <xsd:appinfo>  
             <msdata:relationship  
                     parent="Customers"  
                     parent-key="CustomerID"  
                     child-key="CustomerID"  
                     child="Customers" />  
           </xsd:appinfo>  
         </xsd:annotation>  
       </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
  <xsd:element name="Customers" type="CustomerType"/>  
  <xsd:complexType name="CustomerType">  
    <xsd:complexContent>  
       <xsd:restriction base="CustomerBaseType">  
          <xsd:sequence>  
            <xsd:element name="CID"   
                         type="xsd:string"/>  
            <xsd:element name="CompanyName"   
                         type="xsd:string"  
                         msdata:field="CName" />  
            <xsd:element name="Customers"   
                         type="CustomerType" />  
          </xsd:sequence>  
       </xsd:restriction>  
    </xsd:complexContent>  
  </xsd:complexType>  
</xsd:schema>   
```  
  
 Nello schema `sql:max-depth` viene specificato per un tipo complesso `CustomerBaseType`. Lo schema specifica anche un  **\<cliente >** elemento di tipo `CustomerType`, che deriva da `CustomerBaseType`. Una query XPath specificata per tale schema genererà un errore, in quanto `sql:max-depth` non è supportato per un elemento definito in un tipo restriction di base.  
  
## <a name="schemas-with-a-deep-hierarchy"></a>Schemi con una gerarchia profonda  
 Si potrebbe avere uno schema che include una gerarchia profonda nella quale un elemento contiene un elemento figlio che, a sua volta, contiene un altro elemento figlio e così via. Se l'annotazione `sql:max-depth` specificata in uno schema di questo tipo genera un documento XML che include una gerarchia di più di 500 livelli (con l'elemento di livello superiore al livello 1, il rispettivo figlio al livello 2 e così via), viene restituito un errore.  
  
  
