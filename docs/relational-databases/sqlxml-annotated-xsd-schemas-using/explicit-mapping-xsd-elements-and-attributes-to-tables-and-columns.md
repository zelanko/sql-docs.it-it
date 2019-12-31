---
title: Mapping XSD personalizzati a tabelle/colonne (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fafcd918dda0001c316fd68cae3b19e6cd805a3
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257435"
---
# <a name="custom-xsd-mappings-to-tablescolumns-sqlxml"></a>Mapping XSD personalizzati a tabelle/colonne (SQLXML)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si utilizza uno schema XSD per fornire una vista XML del database relazionale, è necessario eseguire il mapping degli elementi e degli attributi dello schema a tabelle e colonne del database. Le righe della tabella/vista di database vengono mappate agli elementi del documento XML. I valori di colonna del database vengono mappati agli attributi o agli elementi.  
  
 Quando vengono specificate query XPath nello schema XSD con annotazioni, i dati relativi agli elementi e agli attributi dello schema vengono recuperati dalle tabelle e dalle colonne alle quali vengono mappati. Per ottenere un solo valore dal database, per il mapping specificato nello schema XSD devono essere indicati sia la relazione che il campo. Se il nome di un elemento o di un attributo non corrisponde al nome della tabella, della vista o della colonna a cui viene eseguito il mapping, vengono utilizzate le annotazioni **SQL: relation** e **SQL: Field** per specificare il mapping tra un elemento o un attributo in un documento XML e la tabella (vista) o la colonna in un database.  
  
## <a name="sql-relation"></a>sql-relation  
 L'annotazione **SQL: relation** viene aggiunta per eseguire il mapping di un nodo XML nello schema XSD a una tabella di database. Il nome di una tabella (vista) viene specificato come valore dell'annotazione **SQL: relation** .  
  
 Quando **SQL: relation** viene specificato in un elemento, l'ambito di questa annotazione si applica a tutti gli attributi e agli elementi figlio descritti nella definizione del tipo complesso di tale elemento, offrendo quindi un collegamento per la scrittura delle annotazioni.  
  
 L'annotazione **SQL: relation** è utile anche quando gli identificatori validi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in non sono validi in XML. "Order Details", ad esempio, è un nome di tabella valido in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ma non in XML. In questi casi, è possibile usare l'annotazione **SQL: relation** per specificare il mapping, ad esempio:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 L'annotazione **SQL-Field** esegue il mapping di un elemento o di un attributo a una colonna del database. L'annotazione **SQL: Field** viene aggiunta per eseguire il mapping di un nodo XML nello schema a una colonna del database. Non è possibile specificare **SQL: Field** su un elemento di contenuto vuoto.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>R. Specifica delle annotazioni sql:relation e sql:field  
 In questo esempio lo schema XSD è costituito da un ** \<elemento Contact>** di tipo complesso con ** \<fname>** e ** \<lname>** elementi figlio e l'attributo **ContactID** .  
  
 L'annotazione **SQL: relation** esegue il mapping dell' ** \<elemento Contact>** alla tabella Person. Contact del database AdventureWorks. L'annotazione **SQL: Field** esegue il mapping dell' ** \<elemento fname>** alla colonna FirstName e dell' ** \<elemento>lname** alla colonna LastName.  
  
 Non è stata specificata alcuna annotazione per l'attributo **ContactID** . Il risultato ottenuto è un mapping predefinito dell'attributo alla colonna con lo stesso nome.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome MySchema-annotated.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file con il nome MySchema-annotatedT.xml nella stessa directory in cui è stato salvato il file MySchema-annotated.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso della directory specificato per lo schema di mapping MySchema-annotated.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato il set di risultati parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
