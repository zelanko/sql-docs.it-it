---
title: 'Ottenere i riferimenti URL ai dati BLOB con SQL: encode (SQLXML)'
description: "Informazioni su come richiedere un riferimento URL ai dati BLOB specificando l'annotazione sql: Encode in SQLXML 4,0."
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 432b1b888392b345038d14bb18909ba90b4d86a7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461752"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Richiesta di riferimenti URL a dati BLOB utilizzando sql:encode (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  In uno schema XSD con annotazioni quando viene eseguito il mapping di un attributo o elemento a una colonna BLOB in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i dati vengono restituiti in formato con codifica Base 64 in XML.  
  
 Se si vuole che venga restituito un riferimento ai dati (un URI) che possono essere usati in un secondo momento per recuperare i dati BLOB in un formato binario, specificare l'annotazione **SQL: encode** . È possibile specificare **SQL: encode** su un attributo o un elemento di tipo semplice.  
  
 Specificare l'annotazione **SQL: encode** per indicare che deve essere restituito un URL del campo anziché il valore del campo. **SQL: encode** dipende dalla chiave primaria per generare un singleton SELECT nell'URL. La chiave primaria può essere specificata utilizzando l'annotazione **SQL: key-fields** .  
  
 All'annotazione **SQL: encode** è possibile assegnare il valore "URL" o "default". Il valore "default" restituisce dati in formato con codifica Base 64.  
  
 Non è possibile usare l'annotazione **SQL: encode** con **SQL: Use-CDATA** o sui tipi di attributo ID, IDREF, IDREFS, NMTOKEN o NMTOKENS. Non è inoltre possibile utilizzarlo con l'attributo **fixed** XSD.  
  
> [!NOTE]  
>  Non è possibile utilizzare le colonne di tipo BLOB come parte di una chiave o di una chiave esterna.  
  
## <a name="examples"></a>Esempio  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [requisiti per l'esecuzione di esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>R. Specifica di sql:encode per ottenere un riferimento URL ai dati BLOB  
 In questo esempio lo schema di mapping specifica **SQL: encode** sull'attributo **LargePhoto** per recuperare il riferimento URI a una foto del prodotto specifica, anziché recuperare i dati binari nel formato con codifica base 64.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file come sqlEncode.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file come sqlEncodeT.xml nella stessa directory nella quale è stato salvato sqlEncode.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping (sqlEncode.xml) è relativo alla directory nella quale viene salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Risultato:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
