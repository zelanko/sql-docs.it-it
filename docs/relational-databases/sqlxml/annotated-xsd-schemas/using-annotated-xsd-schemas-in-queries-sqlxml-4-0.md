---
title: Utilizzo di schemi XSD con annotazioni nelle query (SQLXML)Using Annotated XSD Schemas in Queries (SQLXML)
description: Informazioni su come specificare query XPath su uno schema XSD con annotazioni in SQLXML 4.0 per recuperare i dati dal database.
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9ecd9d65d0f70f7c25328c15bb886ca52122de2
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388685"
---
# <a name="using-annotated-xsd-schemas-in-queries-sqlxml-40"></a>Utilizzo di schemi XSD con annotazioni in query (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile specificare query su uno schema con annotazioni per recuperare dati dal database specificando in un modello query XPath sullo schema XSD.  
  
 L'elemento ** \<sql:xpath-query>** consente di specificare una query XPath sulla visualizzazione XML definita dallo schema annotato. Lo schema con annotazioni in base al quale deve essere eseguita la query XPath viene identificato utilizzando l'attributo **mapping-schema** dell'elemento ** \<sql:xpath-query>.**  
  
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
  
 È infine possibile creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire la query come parte di un file di modello. Per ulteriori informazioni, vedere [Schemi XDR con annotazioni &#40;deprecati in SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="using-inline-mapping-schemas"></a>Utilizzo di schemi di mapping inline  
 È possibile includere uno schema con annotazioni direttamente in un modello e quindi specificare nel modello una query XPath sullo schema inline. Il modello può essere anche un updategram.  
  
 Un modello può includere più schemi inline. Per utilizzare uno schema inline incluso in un modello, specificare l'attributo **id** con un valore univoco nell'elemento ** \<>xsd:schema,** quindi utilizzare **#idvalue** per fare riferimento allo schema inline. L'attributo **id** è identico nel comportamento all'attributo **sql:id** ( surn:schemas-microsoft-com:xml-sql ) utilizzato negli schemi XDR.  
  
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
  
 Il modello specifica inoltre due query XPath. Ognuno degli ** \<elementi di>xpath-query** identifica in modo univoco lo schema di mapping specificando l'attributo **mapping-schema.**  
  
 Quando si specifica uno schema inline nel modello, l'annotazione **sql:is-mapping-schema** deve essere specificata anche nell'elemento ** \<>xsd:schema.** Lo **schema sql:is-mapping** accetta un valore booleano (0 ,false, 1 , true). Uno schema inline con **sql:is-mapping-schema "1"** viene considerato come schema con annotazioni inline e non viene restituito nel documento XML.  
  
 L'annotazione **sql:is-mapping-schema** appartiene allo spazio dei nomi **modello urn:schemas-microsoft-com:xml-sql**.  
  
 Per testare questo esempio, salvare il modello (InlineSchemaTemplate.xml) in una directory locale, quindi creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello. Per ulteriori informazioni, vedere [Utilizzo di ADO per l'esecuzione di query SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Oltre a specificare l'attributo mapping-schema nell'elemento ** \<sql:xpath-query>** in un modello (quando è presente una query XPath) o in ** \<updg:sync>** elemento in un updategram, è possibile eseguire le operazioni seguenti:In addition to specifying the **mapping-schema** attribute on the sql:xpath-query>element in a template (when there is an XPath query), or on updg:sync>element in an updategram, you can do the following:  
  
-   Specificare l'attributo ** \<** **mapping-schema** nell'elemento ROOT>(dichiarazione globale) nel modello. Questo schema di mapping diventa quindi lo schema predefinito che verrà utilizzato da tutti i nodi XPath e updategram che non dispongono di annotazioni **esplicite dello schema** di mapping.  
  
-   Specificare l'attributo **dello schema** di mapping utilizzando l'oggetto **ADO Command.**  
  
 L'attributo **mapping-schema** specificato nella ** \<>xpath-query** o ** \<updg:sync>** elemento ha la precedenza più alta; l'oggetto **ADO Command** ha la precedenza più bassa.  
  
 Si noti che se si specifica una query XPath in un modello e non si specifica uno schema di mapping su cui viene eseguita la query XPath, la query XPath viene considerata come una query di tipo **dbobject.** Considerare ad esempio il modello seguente:  
  
```  
<sql:xpath-query   
     xmlns:sql="urn:schemas-microsoft-com:xmlsql">  
          Production.ProductPhoto[@ProductPhotoID='100']/@LargePhoto  
</sql:xpath-query>  
```  
  
 Il modello specifica una query XPath ma non specifica uno schema di mapping. Di conseguenza, questa query viene considerata come una query di tipo @ProductPhotoID **dbobject** in cui Production.ProductPhoto è il nome della tabella e '100' è un predicato che trova una foto del prodotto con il valore ID di 100. @LargePhotoè la colonna da cui recuperare il valore.  
  
  
