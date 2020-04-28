---
title: 'Conversione di tipi di dati con SQL: DataType (SQLXML)'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98f2ee047bccf7cd3843fe34aaf8f5caec0dc11a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257471"
---
# <a name="data-type-conversions-and-the-sqldatatype-annotation-sqlxml-40"></a>Conversioni di tipi di dati e annotazione sql: DataType (SQLXML 4,0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In uno schema XSD, l'attributo **xsd: Type** specifica il tipo di dati XSD di un elemento o di un attributo. Quando viene utilizzato uno schema XSD per estrarre dati dal database, il tipo di dati specificato viene utilizzato per formattare i dati.  
  
 Oltre a specificare un tipo XSD in uno schema, è anche possibile specificare un tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati Microsoft utilizzando l'annotazione **SQL: DataType** . Gli attributi **xsd: Type** e **SQL: DataType** controllano il mapping tra tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XSD e tipi di dati.  
  
## <a name="xsdtype-attribute"></a>Attributo xsd:type  
 È possibile utilizzare l'attributo **xsd: Type** per specificare il tipo di dati XML di un attributo o di un elemento mappato a una colonna. **Xsd: Type** influiscono sul documento restituito dal server e sulla query XPath eseguita. Quando viene eseguita una query XPath su uno schema di mapping che contiene **xsd: Type**, XPath utilizza il tipo di dati specificato durante l'elaborazione della query. Per ulteriori informazioni sul modo in cui XPath utilizza **xsd: Type**, vedere [mapping dei tipi di dati XSD ai tipi di dati xpath &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 In un documento restituito tutti i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono convertiti in rappresentazioni di stringa. Alcuni tipi di dati richiedono conversioni aggiuntive. Nella tabella seguente sono elencate le conversioni utilizzate per diversi valori **xsd: Type** .  
  
|Tipo di dati XSD|Conversione SQL Server|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|Data|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Tempo|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Tutti gli altri|Nessuna conversione aggiuntiva|  
  
> [!NOTE]  
>  Alcuni dei valori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiti da potrebbero non essere compatibili con i tipi di dati XML specificati tramite **xsd: Type**, perché la conversione non è possibile, ad esempio la conversione di "xyz" in un tipo di dati **Decimal** , oppure perché il valore supera l'intervallo del tipo di dati (ad esempio,-100000 convertito in un tipo XSD **unsignedShort** ). Conversioni di tipi incompatibili possono restituire documenti XML non validi o errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Mapping dai tipi di dati di SQL Server a tipi di dati XSD  
 Nella tabella seguente viene illustrato un mapping evidente dai tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai tipi di dati XSD. Se il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è noto, nella tabella è disponibile il tipo XSD corrispondente che è possibile specificare nello schema XSD.  
  
|Tipo di dati di SQL Server|Tipo di dati XSD|  
|--------------------------|-------------------|  
|**bigint**|**long**|  
|**binary**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**string**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**string**|  
|**ntext**|**string**|  
|**nvarchar**|**string**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**string**|  
|**sysname**|**string**|  
|**text**|**string**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**string**|  
|**uniqueidentifier**|**string**|  
  
## <a name="sqldatatype-annotation"></a>Annotazione sql:datatype  
 L'annotazione **SQL: DataType** viene utilizzata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificare il tipo di dati. Questa annotazione deve essere specificata nei casi seguenti:  
  
-   Si esegue il caricamento bulk in una colonna **DateTime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un tipo XSD **DateTime**, **date**o **Time** . In questo caso, è necessario identificare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati della colonna tramite **SQL: DataType = "DateTime"**. Questa regola si applica anche agli updategram.  
  
-   Si esegue il caricamento bulk in una colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tipo **uniqueidentifier** e il valore XSD è un GUID che include parentesi graffe ({e}). Quando si specifica **SQL: DataType = "uniqueidentifier"**, le parentesi graffe vengono rimosse dal valore prima che venga inserito nella colonna. Se **SQL: DataType** non è specificato, il valore viene inviato con le parentesi graffe e l'inserimento o l'aggiornamento non riesce.  
  
-   Il tipo di dati XML **base64Binary** esegue il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapping a vari tipi di dati (**Binary**, **Image**o **varbinary**). Per eseguire il mapping del tipo **base64Binary** di dati XML base64Binary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un tipo di dati specifico, utilizzare l'annotazione **SQL: DataType** . Questa annotazione specifica il tipo di dati esplicito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della colonna a cui viene mappato l'attributo. Ciò risulta utile durante l'archiviazione dei dati nei database. Specificando l'annotazione **SQL: DataType** è possibile identificare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati esplicito.  
  
 È in genere consigliabile specificare **SQL: DataType** nello schema.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Definizione dell'attributo xsd:type  
 In questo esempio viene illustrato come un tipo di **Data** XSD specificato utilizzando l'attributo **xsd: Type** nello schema influisca sul documento XML risultante. Lo schema fornisce una vista XML della tabella Sales.SalesOrderHeader nel database AdventureWorks.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 In questo schema XSD sono inclusi tre attributi che restituiscono un valore di data da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esaminare i casi seguenti per lo schema:  
  
-   Specifica **xsd: Type = Date** sull'attributo **OrderDate** . viene visualizzata la parte relativa alla data del valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito da per l'attributo **OrderDate** .  
  
-   Specifica **xsd: Type = Time** nell'attributo **ShipDate** , viene visualizzata la parte relativa all'ora del valore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'attributo **ShipDate** .  
  
-   Non specifica **xsd: Type** sull'attributo **DueDate** . viene visualizzato lo stesso valore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome xsdType.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file con il nome xsdTypeT.xml nella stessa directory in cui è stato salvato xsdType.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (xsdType.xml) è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  

     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato il set di risultati parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 Di seguito viene indicato lo schema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. Definizione del tipo di dati SQL tramite sql:datatype  
 Per un esempio funzionante, vedere l'esempio G in [esempi di caricamento bulk XML &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). In questo esempio viene eseguito il caricamento bulk di un valore GUID che include"{" e "}". Nello schema di questo esempio viene specificato **SQL: DataType** per identificare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il tipo di dati come **uniqueidentifier**. Questo esempio illustra quando è necessario specificare **SQL: DataType** nello schema.  
  
  
