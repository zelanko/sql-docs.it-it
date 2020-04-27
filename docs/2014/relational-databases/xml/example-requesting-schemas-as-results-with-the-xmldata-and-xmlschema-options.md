---
title: 'Esempio: richiesta di schemi di risultato mediante le opzioni XMLDATA e XMLSCHEMA | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, requesting schema example
- RAW mode, with XMLDATA and XMLSCHEMA
ms.assetid: 3504ca38-be66-42b2-8dab-f499c9584840
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2a18dd84f5f0a83cc3c6f42bf664c178c1ba6b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62637927"
---
# <a name="example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options"></a>Esempio: richiesta di schemi di risultato mediante le opzioni XMLDATA e XMLSCHEMA
  La query seguente restituisce lo schema XML-DATA che contiene la descrizione della struttura del documento.  
  
## <a name="example"></a>Esempio  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLDATA  
GO  
```  
  
 Risultato:  
  
```  
<Schema name="Schema1" xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="row" content="empty" model="closed">  
    <AttributeType name="ProductModelID" dt:type="i4" />  
    <AttributeType name="Name" dt:type="string" />  
    <attribute type="ProductModelID" />  
    <attribute type="Name" />  
  </ElementType>  
</Schema>  
<row xmlns="x-schema:#Schema1" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="x-schema:#Schema1" ProductModelID="119" Name="Bike Wash" />  
```  
  
> [!NOTE]
>  <`Schema`> viene considerato come uno spazio dei nomi. Al fine di evitare collisioni a livello di spazi dei nomi quando vengono richiesti più schemi XML-Data in query FOR XML diverse, l'identificatore dello spazio dei nomi, in questo esempio `Schema1` , cambia a ogni esecuzione della query. L'identificatore dello spazio dei nomi è costituito da **Schema_n_** dove **_n_** è un numero intero.  
  
 Specificando l'opzione `XMLSCHEMA` è possibile richiedere lo schema XSD per il risultato.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLSCHEMA  
GO  
```  
  
 Risultato:  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="row">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="119" Name="Bike Wash" />  
  
```  
  
 Come argomento facoltativo di XMLSCHEMA, in FOR XML è possibile specificare l'URI dello spazio dei nomi di destinazione. Nello schema verrà restituito lo spazio dei nomi di destinazione specificato,. che rimane invariato a ogni esecuzione della query. Ad esempio, nella versione modificata, di seguito illustrata, della query precedente è incluso come argomento l'URI dello spazio dei nomi `'urn:example.com'`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML RAW, XMLSCHEMA ('urn:example.com')  
GO  
```  
  
 Risultato:  
  
```  
<xsd:schema targetNamespace="urn:example.com" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="row">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<row xmlns="urn:example.com" ProductModelID="122" Name="All-Purpose Bike Stand" />  
<row xmlns="urn:example.com" ProductModelID="119" Name="Bike Wash" />  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Usare la modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
