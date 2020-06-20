---
title: 'SQL: relationship e regola di ordinamento delle chiavi (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: rothja
ms.author: jroth
ms.openlocfilehash: 10e8dc24c3c9ce234314a793ecdc1c9b41c0f3dd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068215"
---
# <a name="sqlrelationship-and-the-key-ordering-rule-sqlxml-40"></a>sql:relationship e regola di ordinamento delle chiavi (SQLXML 4.0)
  Poiché il caricamento bulk XML genera record quando i nodi entrano nell'ambito e invia tali record a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando i nodi abbandonano l'ambito, i dati per il record devono essere presenti nell'ambito del nodo.  
  
 Si consideri lo schema XSD seguente, in cui la relazione uno-a-molti tra **\<Customer>** **\<Order>** gli elementi e (un cliente può inserire molti ordini) viene specificata tramite l' `<sql:relationship>` elemento:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Quando il **\<Customer>** nodo elemento entra nell'ambito, il caricamento bulk XML genera un record del cliente. Questo record rimane attivo fino a quando il caricamento bulk XML non viene letto **\</Customer>** . Nell'elaborazione del **\<Order>** nodo elemento, il caricamento bulk XML utilizza `<sql:relationship>` per ottenere il valore della colonna chiave esterna CustomerID della tabella CustOrder dall' **\<Customer>** elemento padre, in quanto l' **\<Order>** elemento non specifica l'attributo **CustomerID** . Ciò significa che, nella definizione dell' **\<Customer>** elemento, è necessario specificare l'attributo **CustomerID** nello schema prima di specificare `<sql:relationship>` . In caso contrario, quando un **\<Order>** elemento entra nell'ambito, il caricamento bulk XML genera un record per la tabella CustOrder e quando il caricamento bulk XML raggiunge il **\</Order>** tag di fine, invia il record a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] senza il valore della colonna chiave esterna CustomerID.  
  
 Salvare lo schema fornito in questo esempio come SampleSchema.xml.  
  
### <a name="to-test-a-working-sample"></a>Per testare un esempio reale  
  
1.  Creare le tabelle seguenti:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  Salvare i dati di esempio seguenti come SampleXMLData.xml:  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  Per eseguire il caricamento bulk XML, salvare ed eseguire l'esempio di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic, Scripting Edition (VBScript) seguente come file MySample.vbs:  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     Come risultato, il caricamento bulk XML inserisce un valore NULL nella colonna chiave esterna CustomerID della tabella CustOrder. Se si modificano i dati di esempio XML in modo che l' **\<CustomerID>** elemento figlio venga visualizzato prima dell' **\<Order>** elemento figlio, si ottiene il risultato previsto: il caricamento bulk XML inserisce nella colonna il valore di chiave esterna specificato.  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
                        foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
  
