---
title: Inserimento di dati mediante Updategram XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 52c93c8a30131b1e13ef177d6b76b946a1b639af
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255236"
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>Inserimento di dati mediante updategram XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un updategram indica un'operazione di inserimento quando un'istanza di record è presente il  **\<dopo >** blocco ma non nel corrispondente  **\<prima >** blocco. In questo caso, l'updategram inserisce il record nel  **\<dopo >** blocco nel database.  
  
 Il formato dell'updategram per un'operazione di inserimento è il seguente:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<prima > blocco  
 Il  **\<prima di >** blocco può essere omesso per un'operazione di inserimento. Se l'opzione facoltativa **dello schema di mapping** attributo non è specificato, il  **\<ElementName >** che è stato specificato nell'updategram esegue il mapping a una tabella di database e gli elementi figlio o per eseguire il mapping di attributi colonne della tabella.  
  
## <a name="after-block"></a>\<Dopo aver > blocco  
 È possibile specificare uno o più record nel  **\<dopo >** blocco.  
  
 Se il  **\<dopo >** blocco non fornisce un valore per una determinata colonna, l'updategram utilizza il valore predefinito specificato nello schema con annotazione (se è stato specificato uno schema). Se lo schema non specifica un valore predefinito per la colonna, l'updategram non specifica alcun valore esplicito in questa colonna e, invece, assegna la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (se specificato) valore predefinito per questa colonna. Se non è presente alcun valore predefinito di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e la colonna accetta un valore NULL, l'updategram imposta il valore della colonna su NULL. Se la colonna non ha un valore predefinito e non accetta un valore NULL, il comando non riesce e l'updategram restituisce un errore. L'opzione facoltativa **updg: returnid** attributo viene utilizzato per restituire il valore identity generato dal sistema quando viene aggiunto un record in una tabella con una colonna di tipo IDENTITY.  
  
## <a name="updgid-attribute"></a>Attributo updg:id  
 Se l'updategram inserisce solo record, l'updategram non richiede la **updg: ID** attributo. Per altre informazioni sulle **updg: ID**, vedere [l'aggiornamento di dati mediante Updategram XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md).  
  
## <a name="updgat-identity-attribute"></a>Attributo updg:at-identity  
 Quando un updategram inserisce un record in una tabella che include una colonna di tipo IDENTITY, l'updategram può acquisire il valore assegnato al sistema tramite l'opzione facoltativa **updg: a-identity** attributo. L'updategram potrà quindi utilizzare questo valore nelle operazioni successive. Al termine dell'esecuzione dell'updategram, è possibile restituire il valore identity generato specificando il **updg: returnid** attributo.  
  
## <a name="updgguid-attribute"></a>Attributo updg:guid  
 Il **updg: GUID** attributo è un attributo facoltativo che genera un identificatore univoco globale. Questo valore rimane nell'ambito per l'intera  **\<sync >** blocco in cui è specificato. È possibile usare questo valore in qualsiasi punto nel  **\<sync >** blocco. L'attributo chiama il **NewGuid ()** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] funzione per generare l'identificatore univoco.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare i requisiti specificati nelle [requisiti per l'esecuzione di esempi di SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Prima di utilizzare gli esempi dell'updategram, si tenga presente quanto segue:  
  
-   La maggior parte degli esempi utilizza il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   Nella maggior parte degli esempi viene utilizzato il database di esempio [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]. Tutti gli aggiornamenti vengono applicati alle tabelle di questo database.  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. Inserimento di un record mediante un updategram  
 Questo updategram incentrato sugli attributi inserisce un record nella tabella HumanResources.Employee del database [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].  
  
 In questo esempio l'updategram non specifica uno schema di mapping, pertanto utilizza il mapping predefinito nel quale il nome dell'elemento esegue il mapping a un nome di tabella e gli attributi o gli elementi figlio eseguono il mapping alle colonne della tabella stessa.  
  
 Lo schema di [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] per la tabella HumanResources.Department impone una restrizione 'non null' per tutte le colonne. updategram dovrà pertanto includere i valori specificati per tutte le colonne. DepartmentID è una colonna di tipo IDENTITY, pertanto per tale colonna non viene specificato alcun valore.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome MyUpdategram.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 In un mapping incentrato sugli elementi l'updategram sarà simile al seguente:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 In un updategram in modalità mista (incentrato sugli attributi e incentrato sugli elementi) un elemento può avere sia attributi sia sottoelementi, come mostrato in questo updategram:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>b. Inserimento di più record mediante un updategram  
 Questo updategram aggiunge due nuovi record di spostamento alla tabella HumanResources.Shift. L'updategram non specifica l'opzione facoltativa  **\<prima di >** blocco.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome Updategram-AddShifts.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Un'altra versione di questo esempio è un updategram che utilizza due  **\<dopo >** blocchi anziché un unico blocco per inserire i due dipendenti. Questo updategram è valido e può essere codificato come segue:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. Utilizzo di caratteri validi in SQL Server che non sono validi in XML  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] i nomi di tabella possono includere uno spazio, ad esempio la tabella Dettagli ordine nel database Northwind. Tuttavia, ciò non è valido nei caratteri XML validi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificatori, ma gli identificatori XML non validi possono essere codificati utilizzando ' __xHHHH\_\_' come valore di codifica, dove HHHH rappresenta il codice UCS-2 esadecimale a quattro cifre per il carattere nell'ordine del primo bit più significativo.  
  
> [!NOTE]  
>  In questo esempio viene utilizzato il database Northwind, È possibile installare il database Northwind mediante uno script SQL disponibile per il download da questa [sito Web Microsoft](https://go.microsoft.com/fwlink/?LinkId=30196).  
  
 Inoltre, il nome dell'elemento deve essere racchiuso tra parentesi quadre ([]). Poiché i caratteri [e] non sono validi in XML, è necessario codificarli come _x005B\_ _x005D e\_, rispettivamente. Se si utilizza uno schema di mapping, è possibile fornire nomi di elemento che non contengono caratteri non validi, ad esempio spazi vuoti. Lo schema di mapping esegue il mapping richiesto, pertanto non è necessario eseguire la codifica per questi caratteri.  
  
 Questo updategram aggiunge un record alla tabella Dettagli ordine del database Northwind:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 La colonna UnitPrice della tabella Dettagli ordine è il **denaro** tipo. Per applicare la conversione del tipo appropriato (da un **stringa** tipo di un **denaro** tipo), il carattere di segno di dollaro ($) deve essere aggiunti come parte del valore. Se l'updategram non specifica uno schema di mapping, il primo carattere del **stringa** valore viene valutato. Se il primo carattere è un segno di dollaro ($), viene applicata la conversione appropriata.  
  
 Se l'updategram viene specificato in uno schema di mapping in cui la colonna è contrassegnata in modo appropriato come **dt:type="fixed.14.4"** oppure **SQL: DataType = "money"**, il segno di dollaro ($) non è necessario e il la conversione viene gestita dal mapping. Si tratta della modalità consigliata per garantire che venga eseguita la conversione di tipo appropriata.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome UpdategramSpacesInTableName.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. Utilizzo dell'attributo at-identity per recuperare il valore inserito nella colonna di tipo IDENTITY  
 Nell'updategram seguente sono inseriti due record: uno nella tabella Sales.SalesOrderHeader e un altro nella tabella Sales.SalesOrderDetail.  
  
 L'updategram aggiunge prima un record alla tabella Sales.SalesOrderHeader. In questa tabella la colonna SalesOrderID è una colonna di tipo IDENTITY, Pertanto, quando si aggiunge questo record alla tabella, l'updategram utilizza il **all'identità** attributo per acquisire il valore di SalesOrderID assegnato come "x" (un valore segnaposto). L'updategram specifica quindi questa **in-identity** variabile come valore dell'attributo SalesOrderID nel \<Sales. SalesOrderDetail > elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Se si desidera restituire il valore identity generato dal **updg: in-identity** attributo, è possibile usare il **updg: returnid** attributo. Di seguito viene mostrato un updategram corretto che restituisce questo valore Identity. Per rendere un po' più complesso questo esempio, l'updategram aggiunge due record dell'ordine e due record dei dettagli dell'ordine.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 Quando viene eseguito, l'updategram restituisce risultati simili ai seguenti, che includono il valore Identity generato, ovvero il valore generato della colonna ShiftID utilizzato per l'identità della tabella:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome Updategram-returnId.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. Utilizzo dell'attributo updg:guid per generare un valore univoco  
 In questo esempio l'updategram inserisce un record nelle tabelle Cust e CustOrder. Inoltre, l'updategram genera un valore univoco per l'attributo CustomerID mediante il **updg: GUID** attributo.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 L'updategram specifica il **returnid** attributo. Viene restituito il GUID generato:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome Updategram-GenerateGuid.xml.  
  
2.  Creare le tabelle seguenti:  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. Specifica di uno schema in un updategram  
 In questo esempio l'updategram inserisce un record nella tabella seguente.  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 In questo updategram viene specificato uno schema XSD, ovvero non è presente alcun mapping predefinito degli attributi e degli elementi dell'updategram. Lo schema fornisce il mapping necessario degli elementi e degli attributi alle colonne e alle tabelle di database.  
  
 Lo schema seguente (custorderschema. XML) descrive un  **\<CustOrder >** elemento costituito il **OrderID** e **EmployeeID** attributi. Per rendere più interessante lo schema, viene assegnato un valore predefinito per il **EmployeeID** attributo. Un updategram utilizza il valore predefinito di un attributo solo per le operazioni di inserimento e quindi solo se nell'updategram non è specificato l'attributo in questione.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Questo updategram inserisce un record nella tabella CustOrder. L'updategram specifica solo i valori degli attributi OrderID e EmployeeID. Non specifica il valore dell'attributo OrderType. L'updategram utilizza, pertanto, il valore predefinito dell'attributo EmployeeID specificato nello schema precedente.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 Per ulteriori esempi di updategram che specificano uno schema di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Creare questa tabella la **tempdb** database:  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  Copiare lo schema sopra riportato e incollarlo in un file di testo. Salvare il file con il nome CustOrderSchema.xml.  
  
3.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome CustOrderUpdategram.xml nella stessa cartella utilizzata nel passaggio precedente.  
  
4.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. Utilizzo dell'attributo xsi:nil per inserire valori Null in una colonna  
 Se si desidera inserire un valore null nella colonna corrispondente nella tabella, è possibile specificare il **xsi: nil** attributo su un elemento in un updategram. Nello schema XSD corrispondente, lo schema XSD **nillable** attributo deve anche essere specificato.  
  
 Si consideri, ad esempio, lo schema XSD seguente:  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 Specifica lo schema XSD **nillable = "true"** per il  **\<fname >** elemento. Questo schema viene utilizzato nell'updategram seguente.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 L'updategram non specifica **xsi: nil** per il  **\<fname >** elemento il  **\<dopo >** blocco. pertanto quando questo updategram viene eseguito, viene inserito un valore NULL per la colonna first_name della tabella.  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Creare la tabella seguente nel **tempdb** database:  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  Copiare lo schema sopra riportato e incollarlo in un file di testo. Salvare il file con il nome StudentSchema.xml.  
  
3.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome StudentUpdategram.xml nella stessa cartella utilizzata nel passaggio precedente per salvare il file StudentSchema.xml.  
  
4.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. Specifica degli spazi dei nomi in un updategram  
 In un updategram possono essere presenti elementi che appartengono a uno spazio dei nomi dichiarato nello stesso elemento all'interno dell'updategram. In questo caso anche lo schema corrispondente deve dichiarare lo stesso spazio dei nomi e l'elemento deve appartenere allo spazio dei nomi di destinazione.  
  
 Ad esempio, nell'updategram seguente (UpdateGram-elementhavingnamespace. XML), il  **\<ordine >** elemento appartiene a uno spazio dei nomi dichiarato nell'elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="https://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 In questo caso lo schema deve dichiarare anche lo spazio dei nomi, come mostrato in questo schema:  
  
 Nello schema seguente (XSD-ElementHavingNamespace.xml) viene mostrato come devono essere dichiarati gli attributi e l'elemento corrispondenti.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="https://server/xyz/schemas/"   
     targetNamespace="https://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare lo schema sopra riportato e incollarlo in un file di testo. Salvare il file con il nome XSD-ElementHavingNamespace.xml.  
  
2.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome Updategram-ElementHavingNamespace.xml nella stessa cartella utilizzata per salvare il file XSD-ElementHavingnamespace.xml.  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>I. Inserimento di dati in una colonna con tipo di dati XML  
 Il **xml** tipo di dati è stata introdotta in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. È possibile utilizzare gli updategram per inserire e aggiornare i dati archiviati in **xml** del tipo di dati le colonne con le disposizioni seguenti:  
  
-   Il **xml** colonna non può essere utilizzata per identificare una riga esistente. Pertanto, non può essere inclusa nel **updg: prima** sezione di un updategram.  
  
-   Gli spazi dei nomi inclusi nell'ambito del frammento XML inserito il **xml** colonna verrà mantenuta e le dichiarazioni dello spazio dei nomi vengono aggiunti all'elemento iniziale del frammento inserito.  
  
 Ad esempio, nell'updategram seguente (sampleupdategram. XML), il  **\<Desc >** elemento Aggiorna la colonna ProductDescription della produzione > tabella productModel le [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] database di esempio. Il risultato di questo updategram è che il contenuto XML della colonna ProductDescription viene aggiornato con il contenuto XML del  **\<Desc >** elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="https://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 L'updategram si riferisce allo schema XSD con annotazioni seguente (SampleSchema.xml).  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare lo schema sopra riportato e incollarlo in un file di testo. Salvare il file con il nome XSD-SampleSchema.xml.  
  
    > [!NOTE]  
    >  Poiché gli updategram supportano il mapping predefinito, non è possibile identificare l'inizio e la fine del **xml** tipo di dati. Ciò significa che uno schema di mapping è necessario durante l'inserimento o aggiornamento delle tabelle con **xml** colonne con tipo di dati. Quando non viene fornito uno schema, SQLXML restituisce un errore che indica che nella tabella manca una delle colonne.  
  
2.  Copiare l'updategram sopra riportato e incollarlo in un file di testo. Salvare il file con il nome SampleUpdategram.xml nella stessa cartella utilizzata per salvare il file SampleSchema.xml.  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
