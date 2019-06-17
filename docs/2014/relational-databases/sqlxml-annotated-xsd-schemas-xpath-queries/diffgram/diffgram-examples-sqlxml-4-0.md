---
title: Esempi di DiffGram (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38bee43ed5b727bca552c1b44010dd692012d823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66012966"
---
# <a name="diffgram-examples-sqlxml-40"></a>Esempi di DiffGram (SQLXML 4.0)
  Negli esempi presenti in questo argomento viene illustrato l'utilizzo di DiffGram per eseguire operazioni di inserimento, aggiornamento ed eliminazione nel database. Prima di utilizzare gli esempi, si tenga presente quanto segue:  
  
-   Negli esempi vengono utilizzate due tabelle (Cust e Ord) che devono essere create se si desidera testare gli esempi di DiffGram:  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   La maggior parte degli esempi presenti in questo argomento utilizza lo schema XSD seguente:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     Salvare questo schema con il nome DiffGramSchema.xml nella stessa cartella in cui vengono salvati gli altri file utilizzati negli esempi.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. Eliminazione di un record mediante DiffGram  
 In questo esempio DiffGram viene utilizzato per eliminare un record del cliente (il cui CustomerID è ALFKI) dalla tabella Cust e per eliminare il record dell'ordine corrispondente (il cui OrderID è 1) dalla tabella Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Nel  **\<prima di >** blocca, non vi è un  **\<ordine >** elemento (**diffgr: ID = "Diffgr:ID="Order1"** ) e un  **\< Customer >** elemento (**diffgr: ID = "Customer1"** ). Questi elementi rappresentano i record esistenti nel database. Il  **\<DataInstance >** elemento non ha i record corrispondenti (con lo stesso **diffgr: ID**). indicando un'operazione di eliminazione.  
  
#### <a name="to-test-the-diffgram"></a>Per testare DiffGram  
  
1.  Creare le tabelle nel **tempdb** database.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copiare il DiffGram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyDiffGram.xml nella stessa cartella utilizzata nel passaggio precedente.  
  
4.  Copiare il DiffGramSchema fornito precedentemente in questo argomento e incollarlo in un file di testo. Salvare il file con il nome DiffGramSchema.xml.  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il DiffGram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. Inserimento di un record mediante DiffGram  
 In questo esempio DiffGram viene utilizzato per inserire un record nella tabella Cust e un record nella tabella Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 In questo esempio il  **\<prima di >** blocco non viene specificato (Nessun record di database esistenti identificato). Sono presenti due istanze dei record (identificato dal  **\<cliente >** e  **\<ordine >** elementi nel  **\<DataInstance >** blocchi) che eseguono il mapping alle tabelle Cust e Ord, rispettivamente. Entrambi questi elementi specificano il **diffgr: HasChanges** attributo (**hasChanges = "inserted"** ). indicando un'operazione di inserimento. In questo esempio, se si specifica **hasChanges = "modified"** , si indica che si desidera modificare un record che non esiste, restituirà un errore.  
  
#### <a name="to-test-the-diffgram"></a>Per testare DiffGram  
  
1.  Creare le tabelle nel **tempdb** database.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copiare il DiffGram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyDiffGram.xml nella stessa cartella utilizzata nel passaggio precedente.  
  
4.  Copiare il DiffGramSchema fornito precedentemente in questo argomento e incollarlo in un file di testo. Salvare il file con il nome DiffGramSchema.xml.  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il DiffGram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. Aggiornamento di un record esistente mediante DiffGram  
 In questo esempio DiffGram viene utilizzato per aggiornare le informazioni per il cliente ALFKI (CompanyName e ContactName).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Il  **\<prima di >** blocco include un  **\<cliente >** elemento (**diffgr: ID = "Customer1"** ). Il  **\<DataInstance >** inclusioni di blocco corrispondente  **\<cliente >** elemento con stesso **id**. Il  **\<cliente >** elemento il  **\<NewDataSet >** specifica inoltre **diffgr: HasChanges = "modified"** . Questo indica un'operazione di aggiornamento e il record del cliente nel **Cust** tabella viene aggiornata di conseguenza. Si noti che se il **diffgr: HasChanges** attributo non viene specificato, la logica di elaborazione DiffGram ignora questo elemento e viene eseguito alcun aggiornamento.  
  
#### <a name="to-test-the-diffgram"></a>Per testare DiffGram  
  
1.  Creare le tabelle nel **tempdb** database.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copiare il DiffGram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyDiffGram.xml nella stessa cartella utilizzata nel passaggio precedente.  
  
4.  Copiare il DiffGramSchema fornito precedentemente in questo argomento e incollarlo in un file di testo. Salvare il file con il nome DiffGramSchema.xml.  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il DiffGram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. Inserimento, aggiornamento ed eliminazione di record mediante DiffGram  
 In questo esempio viene utilizzato un DiffGram relativamente complesso per eseguire le operazioni di inserimento, aggiornamento ed eliminazione.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 La logica DiffGram elabora questo DiffGram nel modo seguente:  
  
-   In base alla logica di elaborazione DiffGram, tutti gli elementi principali nel  **\<prima di >** block mappati alle tabelle corrispondenti, come descritto nello schema di mapping.  
  
-   Il  **\<prima di >** blocco ha un  **\<ordine >** elemento (**dffgr:id = "Diffgr:ID="Order1"** ) e un  **\<cliente >** elemento (**diffgr: ID = "Customer1"** ) per cui non esiste alcun elemento corrispondente nel  **\<DataInstance >** blocco (con lo stesso ID). indicando un'operazione di eliminazione e i record vengono eliminati dalle tabelle Cust e Ord.  
  
-   Il  **\<prima di >** blocco ha un  **\<cliente >** elemento (**diffgr: ID = "Customer2"** ) per cui non esiste un corrispondente  **\<Cliente >** elemento di  **\<DataInstance >** blocco (con lo stesso ID). L'elemento di  **\<DataInstance >** blocco specifica **diffgr: HasChanges = "modified"** . Si tratta di un'operazione di aggiornamento in cui per il cliente ANATR, le informazioni CompanyName e ContactName vengono aggiornate nella tabella Cust utilizzando i valori specificati nel  **\<DataInstance >** blocco.  
  
-   Il  **\<DataInstance >** blocco ha un  **\<cliente >** elemento (**diffgr: ID = "Customer3"** ) e un  **\<Ordine >** elemento (**diffgr: ID = "Order3"** ). Nessuno di questi elementi specificare le **diffgr: HasChanges** attributo. Pertanto, la logica di elaborazione di DiffGram ignora tali elementi.  
  
-   Il  **\<DataInstance >** blocco ha un  **\<cliente >** elemento (**diffgr: ID = "Diffgr:ID="customer4"** ) e un  **\<Ordine >** elemento (**diffgr: ID = "Order4"** ) per cui non sono presenti elementi corrispondenti nel \<prima > blocco. Questi elementi nel  **\<DataInstance >** blocco specificare **diffgr: HasChanges = "inserted"** . Pertanto, viene aggiunto un nuovo record nella tabella Cust e nella tabella Ord.  
  
#### <a name="to-test-the-diffgram"></a>Per testare DiffGram  
  
1.  Creare le tabelle seguenti i **tempdb** database.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copiare il DiffGram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyDiffGram.xml nella stessa cartella utilizzata nel passaggio precedente.  
  
4.  Copiare il DiffGramSchema fornito precedentemente in questo argomento e incollarlo in un file di testo. Salvare il file con il nome DiffGramSchema.xml.  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il DiffGram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Applicazione degli aggiornamenti mediante DiffGram con l'annotazione diffgr:parentID  
 Questo esempio viene illustrato come la **parentID** annotation specificato nel  **\<prima >** blocco del DiffGram viene usato nell'applicazione degli aggiornamenti.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 Questo DiffGram specifica un'operazione di eliminazione poiché è presente solo una  **\<prima di >** blocco. Nel DiffGram, il **parentID** annotazione viene usata per specificare una relazione padre-figlio tra gli ordini e dettagli dell'ordine. Quando vengono eliminati i record con SQLXML, questi vengono eliminati prima dalla tabella figlio identificata da questa relazione e poi dalla tabella padre corrispondente.  
  
  
