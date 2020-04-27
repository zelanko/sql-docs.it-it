---
title: Utilizzo di schemi XSD con annotazioni nelle query (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML]
- inline schemas [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- queries [SQLXML], annotated XSD schemas
- retrieving data
- mapping schema [SQLXML], queries
- multiple inline schemas
- annotated XSD schemas, queries
- XSD schemas [SQLXML], queries
- templates [SQLXML], annotated XSD schemas in queries
ms.assetid: 927a30a2-eae8-420d-851d-551c5f884f3c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c435ff3bacecb101784695fe42b8b2158625e058
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014471"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Utilizzo di schemi XSD con annotazioni in query (SQLXML 4.0)
  È possibile specificare query su uno schema con annotazioni per recuperare dati dal database specificando in un modello query XPath sullo schema XSD.  
  
 L' ** \<elemento SQL: XPath-query>** consente di specificare una query XPath sulla vista XML definita dallo schema con annotazioni. Lo schema con annotazioni su cui viene eseguita la query XPath viene identificato tramite l' `mapping-schema` attributo dell'elemento ** \<SQL: XPath-query>** .  
  
 I modelli sono documenti XML validi che contengono una o più query. Le query FOR XML e XPath restituiscono un frammento del documento. I modelli fungono da contenitori per i frammenti del documento e offrono in tal modo un metodo per specificare un singolo elemento di livello principale.  
  
 Negli esempi inclusi in questo argomento vengono utilizzati modelli per specificare una query XPath su uno schema con annotazioni per recuperare dati dal database.  
  
 Si consideri, ad esempio, lo schema con annotazioni seguente:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact" >  
     <xsd:complexType>  
       <xsd:attribute name="ContactID" type="xsd:string" />   
       <xsd:attribute name="FirstName" type="xsd:string" />   
       <xsd:attribute name="LastName"  type="xsd:string" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 A scopo illustrativo, lo schema XSD viene archiviato in un file denominato Schema2.xml. È quindi possibile specificare una query XPath sullo schema con annotazioni nel file di modello seguente (Schema2T.xml):  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql"  
     >  
          Person.Contact[@ContactID="1"]  
</sql:xpath-query>  
```  
  
 È infine possibile creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire la query come parte di un file di modello. Per ulteriori informazioni, vedere [schemi XDR con Annotazioni &#40;deprecati in SQLXML 4,0&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Utilizzo di schemi di mapping inline  
 È possibile includere uno schema con annotazioni direttamente in un modello e quindi specificare nel modello una query XPath sullo schema inline. Il modello può essere anche un updategram.  
  
 Un modello può includere più schemi inline. Per utilizzare uno schema inline incluso in un modello, specificare l'attributo **ID** con un valore univoco nell'elemento ** \<xsd: schema>** , quindi utilizzare **#idvalue** per fare riferimento allo schema inline. Il comportamento dell'attributo **ID** è identico a quello di **SQL: ID** ({urn: schemas-microsoft-com: XML-SQL} ID) utilizzato negli schemi XDR.  
  
 Nel modello seguente, ad esempio, vengono specificati due schemi con annotazioni inline:  
  
```  
<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema1' sql:is-mapping-schema='1'>  
  <xsd:element name='Employees' ms:relation='HumanResources.Employee'>  
    <xsd:complexType>  
      <xsd:attribute name='LoginID'   
                     type='xsd:string'/>  
      <xsd:attribute name='Title'   
                     type='xsd:string'/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<xsd:schema xmlns:xsd='http://www.w3.org/2001/XMLSchema'  
        xmlns:ms='urn:schemas-microsoft-com:mapping-schema'  
        id='InLineSchema2' sql:is-mapping-schema='1'>  
  <xsd:element name='Contacts' ms:relation='Person.Contact'>  
    <xsd:complexType>  
  
      <xsd:attribute name='ContactID'   
                     type='xsd:string' />  
      <xsd:attribute name='FirstName'   
                     type='xsd:string' />  
      <xsd:attribute name='LastName'   
                     type='xsd:string' />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema1'>  
    /Employees[@LoginID='adventure-works\guy1']  
</sql:xpath-query>  
  
<sql:xpath-query xmlns:sql='urn:schemas-microsoft-com:xml-sql'   
        mapping-schema='#InLineSchema2'>  
    /Contacts[@ContactID='1']  
</sql:xpath-query>  
</ROOT>  
```  
  
 Il modello specifica inoltre due query XPath. Ognuno degli elementi ** \<>di query XPath** identifica in modo univoco lo schema di mapping specificando `mapping-schema` l'attributo.  
  
 Quando si specifica uno schema inline nel modello, è necessario `sql:is-mapping-schema` specificare anche l'annotazione nell'elemento ** \<xsd: schema>** . `sql:is-mapping-schema` utilizza un valore booleano (0=false, 1=true). Uno schema inline con **SQL: is-mapping-schema = "1"** viene considerato come schema con annotazioni inline e non viene restituito nel documento XML.  
  
 L'annotazione `sql:is-mapping-schema` appartiene allo spazio dei nomi del modello `urn:schemas-microsoft-com:xml-sql`.  
  
 Per testare questo esempio, salvare il modello (InlineSchemaTemplate.xml) in una directory locale, quindi creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello. Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Oltre a specificare l' `mapping-schema` attributo nell'elemento ** \<SQL: XPath-query>** in un modello (quando è presente una query XPath) o nell'elemento ** \<attributo updg: Sync>** in un updategram, è possibile eseguire le operazioni seguenti:  
  
-   Specificare l' `mapping-schema` attributo nell'elemento ** \<radice>** (dichiarazione globale) nel modello. Questo schema di mapping diventa quindi lo schema predefinito che verrà utilizzato da tutti i nodi XPath e updategram che non dispongono di alcuna annotazione `mapping-schema` esplicita.  
  
-   Specificare l'attributo `mapping schema` utilizzando l'oggetto ADO `Command`.  
  
 L' `mapping-schema` attributo specificato nell'elemento ** \<XPath-query>** o ** \<attributo updg: Sync>** ha la precedenza più elevata; l'oggetto `Command` ADO ha la precedenza più bassa.  
  
 Si noti che se si specifica una query XPath in un modello e non si specifica uno schema di mapping sul quale viene eseguita la query XPath, la query XPath viene considerata come una query di tipo **dbobject** . Considerare ad esempio il modello seguente:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 Il modello specifica una query XPath ma non specifica uno schema di mapping. Questa query viene pertanto considerata una query di tipo **dbobject** in cui Production. ProductPhoto è il nome della tabella @ProductPhotoIDe =' 100' è un predicato che trova una foto del prodotto con valore ID 100. @LargePhotocolonna da cui recuperare il valore.  
  
  
