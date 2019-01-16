---
title: L'aggiornamento dei dati mediante Updategram XML (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0d627b294281e5022cbc2dec34de884ab658318
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256596"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>Aggiornamento di dati tramite updategram XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si aggiornano i dati esistenti, è necessario specificare sia il  **\<prima di >** e  **\<dopo >** blocchi. Gli elementi specificati nel  **\<prima di >** e  **\<dopo >** blocchi descrivono la modifica desiderata. L'updategram utilizza gli elementi specificati nel  **\<prima di >** blocco per identificare i record esistenti nel database. Gli elementi corrispondenti nel  **\<dopo >** blocco indicare come i record devono apparire dopo l'esecuzione dell'operazione di aggiornamento. Da queste informazioni, l'updategram crea un'istruzione SQL che corrisponde alla  **\<dopo >** blocco. L'updategram utilizza quindi questa istruzione per aggiornare il database.  
  
 Di seguito viene illustrato il formato dell'updategram per un'operazione di aggiornamento:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 Gli elementi di  **\<prima di >** blocco identificano record esistenti nelle tabelle del database.  
  
 **\<updg:after>**  
 Gli elementi nel  **\<dopo >** blocco viene descritto come il record specificato nella  **\<prima >** blocco dovrebbe avere un aspetto dopo gli aggiornamenti vengono applicati.  
  
 Il **dello schema di mapping** attributo identifica lo schema di mapping da utilizzare dall'updategram. Se l'updategram specifica uno schema di mapping, i nomi di elementi e attributi specificati nel  **\<prima di >** e  **\<dopo >** blocchi devono corrispondere ai nomi nello schema. Lo schema di mapping esegue il mapping di questi nomi degli elementi o degli attributi ai nomi delle tabelle e delle colonne del database.  
  
 Se un updategram non specifica uno schema, utilizza il mapping predefinito. In un mapping predefinito il  **\<ElementName >** specificato nell'updategram esegue il mapping alla tabella di database e la mappa di elementi o attributi figlio alle colonne del database.  
  
 Un elemento di  **\<prima di >** blocco deve corrispondere con solo una riga di tabella nel database. Se l'elemento corrisponde a più righe della tabella o non corrisponde alcuna riga di tabella, l'updategram restituisce un errore e Annulla l'intera  **\<sync >** blocco.  
  
 Un updategram può includere più  **\<sync >** blocchi. Ciascuna  **\<sync >** blocco viene considerato come una transazione. Ciascuna  **\<sync >** blocco può avere più  **\<prima >** e  **\<dopo >** blocchi. Ad esempio, se si aggiornano due dei record esistenti, è possibile specificare due  **\<prima di >** e  **\<dopo >** coppie, uno per ciascun record aggiornato.  
  
## <a name="using-the-updgid-attribute"></a>Utilizzo dell'attributo updg:id  
 Quando vengono specificati più elementi nel  **\<prima di >** e  **\<dopo >** blocchi, usare il **updg: ID** attributo per contrassegnare le righe nel  **\<prima di >** e  **\<dopo >** blocchi. La logica di elaborazione utilizza queste informazioni per determinare cosa registrare il  **\<prima >** coppie con il record in blocco il  **\<dopo >** blocco.  
  
 Il **updg: ID** attributo non è necessario, sebbene consigliato, in presenza di una delle operazioni seguenti:  
  
-   Gli elementi nello schema di mapping specificato hanno le **SQL: Key-campi** attributo definito su di essi.  
  
-   Per i campi chiave nell'updategram vengono forniti uno o più valori specifici.  
  
 Se è il caso, l'updategram utilizza le colonne chiave specificate nel **SQL: Key-campi** accoppiare gli elementi nel  **\<prima >** e  **\< Dopo aver >** blocchi.  
  
 Se lo schema di mapping non identifica colonne chiave (tramite **SQL: Key-campi**) o se l'updategram aggiorna un valore della colonna chiave, è necessario specificare **updg: ID**.  
  
 I record che sono identificati i  **\<prima >** e  **\<dopo >** blocchi non devono essere nello stesso ordine. Il **updg: ID** attributo forza l'associazione tra gli elementi specificati nel  **\<prima >** e  **\<dopo >** blocchi.  
  
 Se si specifica un elemento nel  **\<prima di >** blocco e solo un elemento corrispondente nel  **\<dopo >** bloccato, tramite **updg: ID** non è necessario. Tuttavia, si consiglia di specificare **updg: ID** comunque per evitare ambiguità.  
  
## <a name="examples"></a>Esempi  
 Prima di utilizzare gli esempi di updategram, tenere presente quanto segue:  
  
-   La maggior parte degli esempi utilizza il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   La maggior parte degli esempi utilizza il database di esempio AdventureWorks. Tutti gli aggiornamenti vengono applicati alle tabelle di questo database. È possibile ripristinare il database AdventureWorks.  
  
### <a name="a-updating-a-record"></a>A. Aggiornamento di un record  
 Nell'updategram seguente il cognome del dipendente viene aggiornato a Fuller nella tabella Person.Contact del database AdventureWorks. Poiché l'updategram non specifica alcuno schema di mapping, utilizza il mapping predefinito.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 Il record è descritto nel  **\<prima >** blocco rappresenta il record corrente nel database. Updategram utilizza tutti i valori della colonna specificati nella  **\<prima >** blocco per cercare il record. In questo updategram, il  **\<prima >** blocco fornisce solo la colonna ContactID; pertanto, utilizza solo il valore di updategram per cercare il record. Se si aggiungesse il valore LastName a questo blocco, l'updategram utilizzerebbe sia i valori ContactID e LastName per la ricerca.  
  
 In questo updategram, il  **\<dopo >** blocco fornisce solo il valore della colonna LastName in quanto questo è l'unico valore che viene modificato.  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare il modello di updategram precedente e incollarlo in un file di testo. Salvare il file con il nome UpdateLastName.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>b. Aggiornamento di più record tramite l'attributo updg:id  
 In questo esempio l'updategram esegue due aggiornamenti nella tabella HumanResources.Shift del database AdventureWorks:  
  
-   L'updategram modifica il nome del turno diurno originale che inizia alle 7.00 da "Day" a "Early Morning".  
  
-   L'updategram inserisce quindi un nuovo turno denominato "Late Morning" che inizia alle 10.00.  
  
 Nell'updategram, il **updg: ID** attributo consente di creare associazioni tra elementi nel  **\<prima >** e  **\<dopo >** blocchi.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Si noti come il **updg:id** coppie di attributo la prima istanza del \<HumanResources.Shift > elemento il  **\<prima >** blocco con la seconda istanza di \< HumanResources.Shift > elemento di  **\<dopo >** blocco.  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare il modello di updategram precedente e incollarlo in un file di testo. Salvare il file con il nome UpdateMultipleRecords.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. Specifica di più \<prima > e \<dopo > blocchi  
 Per evitare ambiguità, è possibile scrivere updategram dell'esempio B utilizzando più  **\<prima >** e  **\<dopo >** bloccare coppie. Se si specifica  **\<prima >** e  **\<dopo >** coppie rappresenta un modo per specificare più aggiornamenti con un minimo di confusione. Inoltre, se ogni del  **\<prima di >** e  **\<dopo >** blocchi specificano al massimo un elemento, non è necessario utilizzare il **updg: ID** attributo .  
  
> [!NOTE]  
>  Per formare una coppia, il  **\<dopo >** tag deve seguire immediatamente il corrispondente  **\<prima >** tag.  
  
 In seguito updategram, la prima  **\<prima >** e  **\<dopo >** coppia aggiorna il nome di spostamento per il turno diurno. La seconda coppia inserisce un record per un nuovo turno.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare il modello di updategram precedente e incollarlo in un file di testo. Salvare il file con il nome UpdateMultipleBeforeAfter.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. Specifica di più \<sync > blocchi  
 È possibile specificare più  **\<sincronizzazione >** blocchi in un updategram. Ogni  **\<sincronizzazione >** blocco specificato è una transazione indipendente.  
  
 In seguito updategram, la prima  **\<sincronizzazione >** blocco aggiorna un record nella tabella Sales. Customer. Per motivi di semplicità, l'updategram specifica solo i valori di colonna obbligatori, ovvero il valore Identity (CustomerID) e il valore da aggiornare (SalesPersonID).  
  
 Il secondo  **\<sincronizzazione >** blocco aggiunge due record alla tabella Sales. SalesOrderHeader. Per questa tabella la colonna SalesOrderID è una colonna di tipo IDENTITY. Pertanto, updategram non specifica il valore SalesOrderID in ciascuno della \<Sales. SalesOrderHeader > elementi.  
  
 Specifica di più  **\<sincronizzazione >** blocchi è utile perché se il secondo  **\<sincronizzazione >** (una transazione) blocco non riesce ad aggiungere record alla tabella Sales. SalesOrderHeader, il prima  **\<sincronizzazione >** blocco ancora possibile aggiornare il record del cliente nella tabella Sales. Customer.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare il modello di updategram precedente e incollarlo in un file di testo. Salvare il file con il nome UpdateMultipleSyncs.xml.  
  
2.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-a-mapping-schema"></a>E. Utilizzo di uno schema di mapping  
 In questo esempio, l'updategram specifica uno schema di mapping mediante la **dello schema di mapping** attributo. Non è disponibile alcun mapping predefinito, ovvero lo schema di mapping fornisce il mapping necessario di elementi e attributi nell'updategram alle tabelle e alle colonne del database.  
  
 Gli elementi e gli attributi specificati nell'updategram fanno riferimento agli elementi e agli attributi nello schema di mapping.  
  
 Il seguente schema di mapping XSD è  **\<cliente >**,  **\<ordine >**, e  **\<OD >** gli elementi associati al Tabelle nel database Sales, Sales. SalesOrderHeader e Sales. SalesOrderDetail.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Questo schema di mapping (UpdategramMappingSchema.xml) viene specificato nell'updategram seguente. L'updategram aggiunge un elemento relativo ai dettagli di un ordine nella tabella Sales.SalesOrderDetail per un ordine specifico. Updategram include elementi nidificati: un  **\<OD >** elemento nidificato all'interno di un  **\<ordine >** elemento. La relazione di chiave primaria/chiave esterna tra questi due elementi viene specificata nello schema di mapping.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare lo schema di mapping precedente e incollarlo in un file di testo. Salvare il file con il nome UpdategramMappingSchema.xml.  
  
2.  Copiare il modello di updategram precedente e incollarlo in un file di testo. Salvare il file con il nome UpdateWithMappingSchema.xml nella stessa cartella utilizzata per salvare lo schema di mapping (UpdategramMappingSchema.xml).  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. Utilizzo di uno schema di mapping con attributi IDREFS  
 In questo esempio viene illustrato il modo in cui gli attributi IDREFS nello schema di mapping vengono utilizzati dagli updategram per aggiornare record in più tabelle. Nell'esempio si presuppone che il database sia costituito dalle tabelle seguenti:  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 Poiché uno studente può iscriversi a molti corsi e un corso può avere molti studenti, la terza tabella, Enrollment, è necessaria per rappresentare questa relazione M:N.  
  
 Il seguente schema di mapping XSD fornisce una visualizzazione XML delle tabelle utilizzando il  **\<Student >**,  **\<corso >**, e  **\<registrazione >** elementi. Il **IDREFS** attributi nello schema di mapping specificano la relazione tra questi elementi. Il **StudentIDList** attributo del  **\<corso >** elemento è un **IDREFS** tipo attributo che fa riferimento alla colonna StudentID nella tabella Enrollment. Allo stesso modo, il **EnrolledIn** attributo del  **\<Student >** elemento è un **IDREFS** tipo attributo che fa riferimento alla colonna CourseID nell'ambito della registrazione tavolo.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Ogni volta che si specifica questo schema in un updategram e si inserisce un record nella tabella Course, l'updategram inserisce un nuovo record di corso nella tabella Course. Se si specificano uno o più nuovi ID studente per l'attributo StudentIDList, l'updategram inserisce inoltre un record nella tabella Enrollment per ogni nuovo studente. L'updategram fa sì che non vengano aggiunti duplicati alla tabella Enrollment.  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Creare le tabelle seguenti nel database specificato nella radice virtuale:  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  Aggiungere i dati di esempio seguenti:  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  Copiare lo schema di mapping precedente e incollarlo in un file di testo. Salvare il file con il nome SampleSchema.xml.  
  
4.  Salvare l'updategram (SampleUpdategram) nella stessa cartella utilizzata per salvare lo schema di mapping nel passaggio precedente. Questo updategram elimina uno studente con StudentID="1" dal corso CS102.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire l'updategram.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
6.  Salvare ed eseguire l'updategram seguente come descritto nei passaggi precedenti. L'updategram aggiunge lo studente con StudentID="1" al corso CS102 tramite l'aggiunta di un record nella tabella Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  Salvare ed eseguire l'updategram successivo come descritto nei passaggi precedenti. L'updategram inserisce tre nuovi studenti e li iscrive al corso CS101. La relazione IDREFS inserisce nuovamente record nella tabella Enrollment.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
