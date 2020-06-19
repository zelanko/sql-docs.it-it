---
title: 'Filtro di valori tramite SQL: limit-field e SQL: Limit-Value (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, filtering values
- limiting values [SQLXML]
- limit-value annotation
- limit-field annotation
- sql:limit-field
- sql:limit-value
- filtering [SQLXML]
ms.assetid: c0f7ae92-eeec-430e-a66a-f22c3ae64a5e
author: rothja
ms.author: jroth
ms.openlocfilehash: 7886a9a6f51c76ed693576ca6f4659f4051d1f20
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063002"
---
# <a name="filtering-values-using-sqllimit-field-and-sqllimit-value-sqlxml-40"></a>Filtrare valori tramite sql:limit-field e sql:limit-value (SQLXML 4.0)
  È possibile limitare le righe restituite da una query di database in base a un valore di limitazione. Le annotazioni `sql:limit-field` e `sql:limit-value` vengono utilizzate per identificare la colonna di database che contiene valori di limitazione e per specificare un valore di limitazione specifico da utilizzare per filtrare i dati restituiti.  
  
 L'annotazione `sql:limit-field` viene utilizzata per identificare una colonna che contiene un valore di limitazione ed è consentita in ciascun elemento o attributo di cui sia stato eseguito il mapping.  
  
 L'annotazione `sql:limit-value` viene utilizzata per specificare il valore limitato nella colonna specificata nell'annotazione `sql:limit-field`. L'annotazione `sql:limit-value` è facoltativa. Se l'annotazione `sql:limit-value` non viene specificata, si presuppone un valore NULL.  
  
> [!NOTE]  
>  Quando si utilizza un'annotazione `sql:limit-field` in cui la colonna SQL mappata è di tipo `real`, SQLXML 4.0 esegue la conversione nell'annotazione `sql:limit-value` specificata negli elementi XML Schema come valore `nvarchar` specificato. Per questa operazione è necessario che i valori del limite decimale siano specificati tramite la notazione scientifica completa. Per ulteriori informazioni, vedere l'esempio B seguente.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando questi esempi, è necessario che siano installati gli elementi seguenti.  
  
-   Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   MDAC 2.6 o versione successiva  
  
 In questi esempi vengono utilizzati modelli per specificare query XPath sullo schema di mapping XSD.  
  
### <a name="a-limiting-the-customer-addresses-returned-to-a-specific-address-type"></a>R. Limitazione degli indirizzi dei clienti restituiti a un tipo di indirizzo specifico  
 In questo esempio un database contiene due tabelle:  
  
-   Customer (CustomerID, CompanyName)  
  
-   Addresses (CustomerID, AddressType, StreetAddress)  
  
 Un cliente può disporre di un indirizzo di spedizione e/o di un indirizzo di fatturazione. I valori della colonna AddressType sono Shipping e Billing.  
  
 Si tratta dello schema di mapping in cui l'attributo dello schema **ShipTo** viene mappato alla colonna StreetAddress nella relazione degli indirizzi. I valori restituiti per questo attributo vengono limitati solo agli indirizzi di spedizione specificando le annotazioni `sql:limit-field` e `sql:limit-value`. Analogamente, l'attributo dello schema **billTo** restituisce solo l'indirizzo di fatturazione di un cliente.  
  
 Lo schema è il seguente:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustAddr"  
        parent="Customer"  
        parent-key="CustomerID"  
        child="Addresses"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Customer" >  
   <xsd:complexType>  
        <xsd:sequence>  
        <xsd:element name="BillTo"   
                       type="xsd:string"   
                       sql:relation="Addresses"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="billing"  
                       sql:relationship="CustAddr" >  
        </xsd:element>  
        <xsd:element name="ShipTo"   
                       type="xsd:string"   
                       sql:relation="Addresses"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="shipping"  
                       sql:relationship="CustAddr" >  
        </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:int" />   
        <xsd:attribute name="CompanyName"  type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Creare due tabelle nel database **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Customer (CustomerID int primary key,   
                           CompanyName varchar(30))  
    CREATE TABLE Addresses(CustomerID int,   
                           StreetAddress varchar(50),  
                           AddressType varchar(10))  
    ```  
  
2.  Aggiungere i dati di esempio:  
  
    ```  
    INSERT INTO Customer values (1, 'Company A')  
    INSERT INTO Customer values (2, 'Company B')  
  
    INSERT INTO Addresses values  
               (1, 'Obere Str. 57 Berlin', 'billing')  
    INSERT INTO Addresses values  
               (1, 'Avda. de la Constituci??n 2222 M??xico D.F.', 'shipping')  
    INSERT INTO Addresses values  
               (2, '120 Hanover Sq., London', 'billing')  
    INSERT INTO Addresses values  
               (2, 'Forsterstr. 57, Mannheim', 'shipping')  
    ```  
  
3.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome LimitFieldValue.xml.  
  
4.  Creare il modello seguente (LimitFieldValueT.xml) e salvarlo nello stesso percorso in cui è stato salvato lo schema (LimitFieldValue.xml) nel passaggio precedente:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="LimitFieldValue.xml">  
            /Customer  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (LimitFieldValue.xml) è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\LimitFieldValue.xml"  
    ```  
  
5.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Risultato:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1" CompanyName="Company A">   
     <BillTo>Obere Str. 57 Berlin</BillTo>   
     <ShipTo>Avda. de la Constituci??n 2222 M??xico D.F.</ShipTo>   
  </Customer>   
  <Customer CustomerID="2" CompanyName="Company B">   
     <BillTo>120 Hanover Sq., London</BillTo>   
     <ShipTo>Forsterstr. 57, Mannheim</ShipTo>   
   </Customer>   
</ROOT>  
```  
  
### <a name="b-limiting-results-based-on-a-discount-value-of-type-real-data"></a>B. Limitare i risultati in base a un valore di sconto con tipo di dati real  
 In questo esempio un database contiene due tabelle:  
  
-   Orders (OrderID)  
  
-   OrderDetails (OrderID, ProductID, UnitPrice, Quantity, Price, Discount)  
  
 Si tratta dello schema di mapping in cui l'attributo **OrderID** sui dettagli dell'ordine viene mappato alla colonna OrderID nella relazione Orders. I valori restituiti per questo attributo sono limitati solo a quelli con valore pari 2.0000000 e-001 (0,2) come specificato per l'attributo **discount** usando le `sql:limit-field` `sql:limit-value` annotazioni e.  
  
 Lo schema è il seguente:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
   <xsd:appinfo>  
    <sql:relationship name="OrderOrderDetails"  
        parent="Orders"  
        parent-key="OrderID"  
        child="OrderDetails"  
        child-key="OrderID" />  
   </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="root" sql:is-constant="1">  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="Order" sql:relation="Orders" >  
          <xsd:complexType>  
             <xsd:sequence>  
                <xsd:element name="orderDetail"   
                       sql:relation="OrderDetails"   
                       sql:limit-field="Discount"                       sql:limit-value="2.0000000e-001"  
                       sql:relationship="OrderOrderDetails">  
                   <xsd:complexType>  
                     <xsd:attribute name="OrderID"   />   
                     <xsd:attribute name="ProductID" />   
                     <xsd:attribute name="Discount"  />   
                     <xsd:attribute name="Quantity"  />   
                     <xsd:attribute name="UnitPrice" />   
                   </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
           <xsd:attribute name="OrderID"/>   
          </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Creare due tabelle nel database **tempdb** :  
  
    ```  
    USE tempdb  
    CREATE TABLE Orders ([OrderID] int NOT NULL ) ON [PRIMARY]  
    ALTER TABLE Orders WITH NOCHECK ADD   
    CONSTRAINT [PK_Orders] PRIMARY KEY  CLUSTERED (  
       [OrderID]  
     )  ON [PRIMARY]   
    CREATE TABLE [OrderDetails] (  
       [OrderID] int NOT NULL ,  
       [ProductID] int NOT NULL ,  
       [UnitPrice] money NULL ,  
       [Quantity] smallint NOT NULL ,  
       [Discount] real NOT NULL   
    ) ON [PRIMARY]  
    ```  
  
2.  Aggiungere i dati di esempio:  
  
    ```  
    INSERT INTO Orders ([OrderID]) values (10248)  
    INSERT INTO Orders ([OrderID]) values (10250)  
    INSERT INTO Orders ([OrderID]) values (10251)  
    INSERT INTO Orders ([OrderID]) values (10257)  
    INSERT INTO Orders ([OrderID]) values (10258)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10248,11,14,12,0)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10250,51,42.4,35,0.15)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10251,22,16.8,6,0.05)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10257,77,10.4,15,0)  
    INSERT INTO [OrderDetails] ([OrderID],[ProductID],[UnitPrice],[Quantity],[Discount]) values (10258,2,15.2,50,0.2)  
    ```  
  
3.  Salvare lo schema (LimitFieldValue.xml) in una directory.  
  
4.  Creare lo script di test seguente (TestQuery.vbs), modificare MyServer nel nome del computer SQL Server e salvarlo nella stessa directory utilizzata nel passaggio precedente per salvare lo schema:  
  
    ```  
    Set conn = CreateObject("ADODB.Connection")  
    conn.Open "Provider=SQLOLEDB;Data Source=MyServer;Database=tempdb;Integrated Security=SSPI"  
    conn.Properties("SQLXML Version") = "sqlxml.4.0"   
    Set cmd = CreateObject("ADODB.Command")  
    Set stm = CreateObject("ADODB.Stream")  
    Set cmd.ActiveConnection = conn  
    stm.open  
    result ="none"  
    strXPathQuery="/root"  
    DBGUID_XPATH = "{EC2A4293-E898-11D2-B1B7-00C04F680C56}"  
    cmd.Dialect = DBGUID_XPATH  
    cmd.CommandText = strXPathQuery  
    cmd.Properties("Mapping schema") = "LimitFieldReal.xml"  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    WScript.Echo "executing for xml query"  
    On Error Resume Next  
    cmd.Execute , ,1024  
    if err then  
    Wscript.Echo err.description  
    Wscript.Echo err.Number  
    Wscript.Echo err.source  
    On Error GoTo 0  
    else  
    stm.Position = 0  
    result  = stm.ReadText  
    end if  
    WScript.Echo result  
    Wscript.Echo "done"  
    ```  
  
5.  Eseguire il file TestQuery.vbs facendovi clic sopra in Esplora risorse.  
  
     Risultato:  
  
    ```  
    <root>  
      <Order OrderID="10248"/>  
      <Order OrderID="10250"/>  
      <Order OrderID="10251"/>  
      <Order OrderID="10257"/>  
      <Order OrderID="10258">  
        <orderDetail OrderID="10258"   
                     ProductID="2"   
                     Discount="0.2"   
                     Quantity="50"/>  
      </Order>  
    </root>  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [&#41;Transact-SQL float e Real &#40;](/sql/t-sql/data-types/float-and-real-transact-sql)   
 [nchar e nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)   
 [Installazione di SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [Utilizzo di schemi XSD con annotazioni nelle query &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml/annotated-xsd-schemas/using-annotated-xsd-schemas-in-queries-sqlxml-4-0.md)  
  
  
