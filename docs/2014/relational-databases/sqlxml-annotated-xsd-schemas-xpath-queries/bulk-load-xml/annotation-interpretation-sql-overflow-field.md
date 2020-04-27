---
title: 'SQL: overflow-field (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594ebdbad3968ba2efe7e255b28379194d2fb77f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013466"
---
# <a name="sqloverflow-field-sqlxml-40"></a>sql:overflow-field (SQLXML 4.0)
  In uno schema è possibile identificare una colonna come colonna di overflow per ricevere tutti i dati non utilizzati dal documento XML. Questa colonna viene specificata nello schema mediante l'annotazione `sql:overflow-field`. È possibile avere più colonne di overflow.  
  
 Ogni volta che un nodo XML (elemento o attributo) per il quale è presente un'annotazione `sql:overflow-field` definita entra in ambito, la colonna di overflow viene attivata e riceve i dati non utilizzati. Quando il nodo non è più in ambito, la colonna di overflow non è più attiva e il caricamento bulk XML rende attivo il campo di overflow precedente, se presente.  
  
 Dopo l'archiviazione dei dati nella colonna di overflow, il caricamento bulk XML archivia anche i tag di apertura e di chiusura dell'elemento padre per il quale viene definito `sql:overflow-field`.  
  
 Nello schema seguente, ad esempio, vengono descritti gli ** \<elementi Customers>** e ** \<CustOrder>** . Ognuno di questi elementi identifica una colonna di overflow:  
  
```  
<?xml version="1.0" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
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
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
               </xsd:complexType>  
             </xsd:element>  
          </xsd:sequence>   
        </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 Nello schema, l' ** \<elemento Customer>** viene mappato alla tabella Cust e l' ** \<elemento Order>** viene mappato alla tabella CustOrder.  
  
 Gli ** \<elementi Customer>** e ** \<Order>** identificano una colonna di overflow. Pertanto, il caricamento bulk XML salva tutti gli attributi e gli elementi figlio non utilizzati dell'elemento ** \<Customer>** nella colonna di overflow della tabella Cust e tutti gli attributi e gli elementi figlio non utilizzati dell'elemento ** \<Order>** nella colonna di overflow della tabella CustOrder.  
  
### <a name="to-test-a-working-sample"></a>Per testare un esempio reale  
  
1.  Salvare lo schema fornito in questo esempio come SampleSchema.xml.  
  
2.  Creare le tabelle seguenti:  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  Salvare i dati XML di esempio seguenti come file SampleXMLData.xml:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
          <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
     </Customers>  
     <Customers>  
       <CustomerID>1112</CustomerID>  
       <CompanyName>Toms Spezialitten</CompanyName>  
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Per eseguire il caricamento bulk XML, salvare ed eseguire questo esempio di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic, Scripting Edition (VBScript) come file Sample.vbs:  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
