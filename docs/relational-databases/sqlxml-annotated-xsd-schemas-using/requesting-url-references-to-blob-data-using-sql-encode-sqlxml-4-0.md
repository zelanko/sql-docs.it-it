---
title: 'Richiesta di riferimenti URL a dati BLOB utilizzando sql: encode (SQLXML 4.0) | Documenti di Microsoft'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fe54541e6f6f86b712e87c73cabc4ac6c4064181
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028532"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Richiesta di riferimenti URL a dati BLOB utilizzando sql:encode (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In uno schema XSD con annotazioni quando viene eseguito il mapping di un attributo o elemento a una colonna BLOB in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i dati vengono restituiti in formato con codifica Base 64 in XML.  
  
 Se si vuole aggiungere un riferimento ai dati (un URI) deve essere restituito che possa essere utilizzato successivamente per recuperare i dati BLOB in un formato binario, specificare il **sql: encode** annotazione. È possibile specificare **sql: encode** su un attributo o elemento di tipo semplice.  
  
 Specificare il **sql: encode** annotazione per indicare che deve essere restituito un URL per il campo anziché il valore del campo. **SQL: encode** dipende dalla chiave primaria per la generazione di una selezione singleton nell'URL. La chiave primaria può essere specificata usando il **SQL: Key-campi** annotazione.  
  
 Il **sql: encode** annotazione può essere assegnata il valore "default" o "url". Il valore "default" restituisce dati in formato con codifica Base 64.  
  
 Il **sql: encode** annotazione non può essere utilizzata con **SQL: use-cdata** o sull'ID, IDREF, IDREFS, NMTOKEN o NMTOKENS tipi di attributo. Può anche non essere utilizzato con XSD **fissa** attributo.  
  
> [!NOTE]  
>  Non è possibile utilizzare le colonne di tipo BLOB come parte di una chiave o di una chiave esterna.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per altre informazioni, vedere [requisiti per l'esecuzione di esempi di SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. Specifica di sql:encode per ottenere un riferimento URL ai dati BLOB  
 In questo esempio, lo schema di mapping specifica **sql: encode** nel **LargePhoto** attributo da recuperare il riferimento URI a una specifica fotografia di prodotto (invece di recuperare i dati binari in Base 64 formato con codifica).  
  
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
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Questo è il risultato:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
