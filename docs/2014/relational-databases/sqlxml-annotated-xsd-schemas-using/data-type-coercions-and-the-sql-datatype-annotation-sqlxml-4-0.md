---
title: 'Coercizioni dei tipi di dati e annotazione sql: DataType (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: d2c4d515540f144052214627b3d6b08211358bb3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013947"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Coercizioni dei tipi di dati e annotazione sql:datatype (SQLXML 4.0)
  In uno schema XDR l'attributo `xsd:type` specifica il tipo di dati XSD di un elemento o di un attributo. Quando viene utilizzato uno schema XSD per estrarre dati dal database, il tipo di dati specificato viene utilizzato per formattare i dati.  
  
 Oltre a specificare un tipo XSD in uno schema, è inoltre possibile specificare un tipo di dati di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'annotazione `sql:datatype`. Le annotazioni `xsd:type` e `sql:datatype` controllano il mapping tra i tipi di dati XSD e i tipi di dati di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="xsdtype-attribute"></a>Attributo xsd:type  
 È possibile utilizzare l'attributo `xsd:type` per specificare il tipo di dati XML di un attributo o di un elemento con mapping a una colonna. 
  `xsd:type` influisce sul documento restituito dal server nonché sulla query XPath eseguita. Quando viene eseguita una query XPath su uno schema di mapping contenente `xsd:type`, XPath utilizza il tipo di dati specificato durante l'elaborazione della query. Per ulteriori informazioni sull'utilizzo `xsd:type`di XPath, vedere [mapping dei tipi di dati XSD ai tipi di dati xpath &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
 In un documento restituito tutti i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono convertiti in rappresentazioni di stringa. Alcuni tipi di dati richiedono conversioni aggiuntive. Nella tabella seguente sono elencate le conversioni utilizzate per i diversi valori di `xsd:type`.  
  
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
>  Alcuni dei valori restituiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbero non essere compatibili con i tipi di dati XML specificati tramite `xsd:type`, in quanto la conversione non è possibile (ad esempio, la conversione di "XYZ" in un tipo di dati `decimal` ) o perché il valore supera l'intervallo del tipo di dati (ad esempio, la conversione di -100000 in un tipo XSD `UnsignedShort`). Conversioni di tipi incompatibili possono restituire documenti XML non validi o errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Mapping dai tipi di dati di SQL Server a tipi di dati XSD  
 Nella tabella seguente viene illustrato un mapping evidente dai tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai tipi di dati XSD. Se il tipo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è noto, nella tabella è disponibile il tipo XSD corrispondente che è possibile specificare nello schema XSD.  
  
|Tipo di dati di SQL Server|Tipo di dati XSD|  
|--------------------------|-------------------|  
|`bigint`|`long`|  
|`binary`|`base64Binary`|  
|`bit`|`boolean`|  
|`char`|`string`|  
|`datetime`|`dateTime`|  
|`decimal`|`decimal`|  
|`float`|`double`|  
|`image`|`base64Binary`|  
|`int`|`int`|  
|`money`|`decimal`|  
|`nchar`|`string`|  
|`ntext`|`string`|  
|`nvarchar`|`string`|  
|`numeric`|`decimal`|  
|`real`|`float`|  
|`smalldatetime`|`dateTime`|  
|`smallint`|`short`|  
|`smallmoney`|`decimal`|  
|`sql_variant`|`string`|  
|`sysname`|`string`|  
|`text`|`string`|  
|`timestamp`|`dateTime`|  
|`tinyint`|`unsignedByte`|  
|`varbinary`|`base64Binary`|  
|`varchar`|`string`|  
|`uniqueidentifier`|`string`|  
  
## <a name="sqldatatype-annotation"></a>Annotazione sql:datatype  
 L'annotazione `sql:datatype` viene utilizzata per indicare il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve essere specificata nei casi seguenti:  
  
-   Si esegue il caricamento bulk in `dateTime` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una colonna da un `dateTime`tipo `date`XSD, `time` o. In questo caso, è necessario identificare il tipo di dati della colonna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando `sql:datatype="dateTime"`. Questa regola si applica anche agli updategram.  
  
-   Si esegue il caricamento bulk in una colonna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `uniqueidentifier` di tipo e il valore XSD è un GUID che include parentesi graffe ({e}). Quando si specifica `sql:datatype="uniqueidentifier"`, le parentesi graffe vengono rimosse dal valore prima che questo venga inserito nella colonna. Se non si specifica `sql:datatype`, il valore viene inviato con le parentesi graffe e l'inserimento o l'aggiornamento non viene eseguito.  
  
-   Viene eseguito il mapping del tipo di dati XML `base64Binary` a diversi tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`binary`, `image` o `varbinary`). Per eseguire il mapping del tipo di dati XML `base64Binary` a un tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifico, utilizzare l'annotazione `sql:datatype`. Questa annotazione specifica il tipo di dati esplicito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] della colonna a cui viene mappato l'attributo. Ciò risulta utile durante l'archiviazione dei dati nei database. Specificando l'annotazione `sql:datatype`, è possibile identificare il tipo di dati esplicito di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È in genere consigliabile specificare `sql:datatype` nello schema.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>R. Definizione dell'attributo xsd:type  
 In questo esempio viene illustrato il modo in cui un tipo XSD `date` specificato tramite l'attributo `xsd:type` nello schema influisce sul documento XML risultante. Lo schema fornisce una vista XML della tabella Sales.SalesOrderHeader nel database AdventureWorks.  
  
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
  
-   Specifica `xsd:type=date` sull'attributo **OrderDate** , viene visualizzata la parte relativa alla data del valore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito da per l'attributo **OrderDate** .  
  
-   Specifica `xsd:type=time` nell'attributo **ShipDate** , viene visualizzata la parte relativa all'ora del valore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'attributo **ShipDate** .  
  
-   Non specifica `xsd:type` sull'attributo **DueDate** , viene visualizzato lo stesso valore restituito da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
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
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
 Per un esempio funzionante, vedere l'esempio G in [esempi di caricamento bulk XML &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). In questo esempio viene eseguito il caricamento bulk di un valore GUID che include"{" e "}". Lo schema in questo esempio specifica `sql:datatype` per identificare il tipo di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come `uniqueidentifier`. In questo esempio vengono indicati i casi in cui è necessario specificare `sql:datatype` nello schema.  
  
  
