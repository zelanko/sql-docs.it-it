---
title: Specifica di uno spazio dei nomi di destinazione mediante l'attributo targetNamespace (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
author: rothja
ms.author: jroth
ms.openlocfilehash: 70ef3dc9bcaf3a839d6164be143e3a90f6d2dd73
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003079"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>Specifica di uno spazio dei nomi di destinazione mediante l'attributo targetNamespace (SQLXML 4.0)
  Per la scrittura di schemi XSD, è possibile utilizzare l'attributo **TARGETNAMESPACE** XSD per specificare uno spazio dei nomi di destinazione. In questo argomento viene descritto il funzionamento degli attributi XSD **targetNamespace**, **elementFormDefault**e **attributeFormDefault** , il modo in cui influiscono sull'istanza XML generata e come vengono specificate le query XPath con gli spazi dei nomi.  
  
 È possibile utilizzare l'attributo **xsd: targetNamespace** per inserire gli elementi e gli attributi dello spazio dei nomi predefinito in uno spazio dei nomi diverso. È inoltre possibile specificare se gli elementi e gli attributi dello schema dichiarati localmente devono essere qualificati da uno spazio dei nomi, sia in modo esplicito mediante un prefisso sia in modo implicito per impostazione predefinita. È possibile usare gli attributi **elementFormDefault** e **attributeFormDefault** sull' **\<xsd:schema>** elemento per specificare a livello globale la qualificazione di elementi e attributi locali oppure è possibile usare l'attributo **form** per specificare separatamente i singoli elementi e attributi.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-a-target-namespace"></a>R. Specificare uno spazio dei nomi di destinazione  
 Nello schema XSD seguente viene specificato uno spazio dei nomi di destinazione utilizzando l'attributo **xsd: targetNamespace** . Lo schema imposta anche i valori degli attributi **elementFormDefault** e **attributeFormDefault** su **"unqualified"** (il valore predefinito per questi attributi). Si tratta di una dichiarazione globale che interessa tutti gli elementi locali ( **\<Order>** nello schema) e gli attributi (**CustomerID**, **ContactName**e **OrderID** nello schema).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 Nello schema:  
  
-   Le dichiarazioni di tipo **CustomerType** e **OrderType** sono globali e, pertanto, sono incluse nello spazio dei nomi di destinazione dello schema. Di conseguenza, quando a questi tipi viene fatto riferimento nella dichiarazione dell' **\<Customer>** elemento e del relativo **\<Order>** elemento figlio, viene specificato un prefisso associato allo spazio dei nomi di destinazione.  
  
-   L' **\<Customer>** elemento viene inoltre incluso nello spazio dei nomi di destinazione dello schema poiché è un elemento globale nello schema.  
  
 Eseguire sullo schema la query Xpath seguente:  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 La query XPath genera questo documento dell'istanza (sono mostrati solo alcuni ordini):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 Questo documento di istanza definisce lo spazio dei nomi urn: MyNamespace e vi associa un prefisso (y0). Il prefisso viene applicato solo all' **\<Customer>** elemento globale. L'elemento è globale perché è dichiarato come elemento figlio dell' **\<xsd:schema>** elemento nello schema.  
  
 Il prefisso non viene applicato agli elementi e agli attributi locali poiché il valore degli attributi **elementFormDefault** e **attributeFormDefault** è impostato su **"unqualified"** nello schema. Si noti che l' **\<Order>** elemento è locale perché la relativa dichiarazione appare come elemento figlio dell' **\<complexType>** elemento che definisce l' **\<CustomerType>** elemento. Analogamente, gli attributi (**CustomerID**, **OrderID**e **ContactName**) sono locali e non globali.  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>Per creare un esempio reale di questo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome targetNameSpace.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file come targetNameSpaceT.xml nella stessa directory nella quale è stato salvato targetNamespace.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La query XPath nel modello restituisce l' **\<Customer>** elemento per il cliente con CustomerID 1. Notare che la query XPath specifica il prefisso dello spazio dei nomi per l'elemento nella query e non per l'attributo. Gli attributi locali non sono qualificati, come specificato nello schema.  
  
     Il percorso di directory specificato per lo schema di mapping (targetNamespace.xml) è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Se lo schema specifica gli attributi **elementFormDefault** e **attributeFormDefault** con il valore **"qualified"**, il documento dell'istanza disporrà di tutti gli elementi e gli attributi locali qualificati. È possibile modificare lo schema precedente in modo da includere questi attributi nell' **\<xsd:schema>** elemento ed eseguire nuovamente il modello. Poiché ora anche gli attributi sono qualificati nell'istanza, la query XPath verrà modificata per includere il prefisso dello spazio dei nomi.  
  
 La query XPath modificata è:  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 Di seguito è riportato il documento XML restituito:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
