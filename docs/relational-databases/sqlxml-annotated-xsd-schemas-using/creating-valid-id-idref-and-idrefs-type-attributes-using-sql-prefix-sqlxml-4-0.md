---
title: 'Attributi ID validi con SQL: prefix (SQLXML)'
description: 'Informazioni su come creare attributi di tipo ID, IDREF e IDREFS validi utilizzando SQL: prefix (SQLXML 4,0).'
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 832607a376c8c08dbcdcff0c70278401a166a7f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750810"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>Creazione di attributi di tipo ID, IDREF e IDREFS validi mediante sql:prefix (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  È possibile specificare un attributo come attributo di tipo ID. Gli attributi specificati come IDREF o IDREFS possono essere quindi utilizzati per fare riferimento agli attributi di tipo ID, in modo da abilitare i collegamenti tra i documenti.  
  
 ID, IDREF e IDREFS corrispondono alle relazioni PK/FK (chiave primaria/chiave esterna) nel database, con poche differenze. In un documento XML i valori degli attributi di tipo ID devono essere distinti. Se gli attributi **CustomerID** e **OrderID** vengono specificati come tipo di ID in un documento XML, questi valori devono essere distinti. In un database, tuttavia, le colonne CustomerID e OrderID possono avere gli stessi valori, ad esempio CustomerID = 1 e OrderID = 1.  
  
 Per specificare attributi ID, IDREF e IDREFS validi:  
  
-   Il valore di ID deve essere univoco all'interno del documento XML.  
  
-   Per ogni IDREF e IDREFS, i valori ID di riferimento devono trovarsi nel documento XML.  
  
-   Il valore di un ID, IDREF e IDREFS deve essere un token denominato. Il valore integer 101, ad esempio, non può essere un valore ID.  
  
-   Non è possibile eseguire il mapping degli attributi di tipo ID, IDREF e IDREFS a colonne di tipo **Text**, **ntext**o **Image** o qualsiasi altro tipo di dati binario (ad esempio, **timestamp**).  
  
 Se un documento XML contiene più ID, utilizzare l'annotazione **SQL: prefix** per assicurarsi che i valori siano univoci.  
  
 Si noti che non è possibile usare l'annotazione **SQL: prefix** con l'attributo fixed XSD.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-id-and-idrefs-types"></a>R. Specifica di tipi ID e IDREFS  
 Nello schema seguente l' **\<Customer>** elemento è costituito dall' **\<Order>** elemento figlio. L'elemento **\<Order>** include anche un elemento figlio, l' **\<OrderDetail>** elemento.  
  
 L'attributo **OrderID** di **\<Customer>** è un attributo di tipo IDREFS che fa riferimento all'attributo **OrderID** dell' **\<Order>** elemento.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
                 parent="Sales.Customer"  
                 parent-key="CustomerID"  
                 child="Sales.SalesOrderHeader"  
                 child-key="CustomerID" />  
    <sql:relationship name="OrderOrderDetail"  
                 parent="Sales.SalesOrderHeader"  
                 parent-key="SalesOrderID"  
                 child="Sales.SalesOrderDetail"  
                 child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
               sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                   sql:relationship="OrderOrderDetail"   
                   maxOccurs="unbounded" >  
                  <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="ProductID" type="xsd:string" />  
                   <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
               </xsd:element>  
             </xsd:sequence>  
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file come sqlPrefix.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file come sqlPrefixT.xml nella stessa directory nella quale è stato salvato sqlPrefix.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (sqlPrefix.xml) è relativo alla directory nella quale viene salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Risultato parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
