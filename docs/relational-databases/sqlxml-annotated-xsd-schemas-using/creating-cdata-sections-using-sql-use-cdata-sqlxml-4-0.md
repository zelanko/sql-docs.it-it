---
title: Creazione di sezioni CDATA utilizzando sql:use-cdata (SQLXML)Creating CDATA sections using sql:use-cdata (SQLXML)
description: Informazioni su come creare sezioni CDATA in SQLXML 4.0 utilizzando l'annotazione sql:use-cdata per eseguire l'escape di blocchi di testo contenenti caratteri di markup.
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aa359c1c1e855c3652d7c6486d3993f588bae46d
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388199"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Creazione di sezioni CDATA mediante sql:use-cdata (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In XML vengono utilizzate le sezioni CDATA per eseguire l'escape di blocchi di testo contenenti caratteri che, altrimenti, verrebbero riconosciuti come caratteri di markup.  
  
 Un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Microsoft può talvolta contenere caratteri che vengono trattati come caratteri di markup dal parser XML; ad esempio, le parentesi angolari (< e >), il simbolo minore di o uguale a (<) e la e commerciale (&) vengono considerati come caratteri di markup. Per evitare che ciò accada, è tuttavia possibile eseguire il wrapping di questo tipo di caratteri speciali in una sezione CDATA. Il testo nella sezione CDATA viene considerato testo normale dal parser XML.  
  
 L'annotazione **sql:use-cdata** viene utilizzata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificare che i dati restituiti da devono essere sottoposti a wrapping in una sezione CDATA , ovvero indica se il valore di una colonna specificata da **sql:field** deve essere racchiuso in una sezione CDATA. L'annotazione **sql:use-cdata** può essere specificata solo su elementi che eseguono il mapping a una colonna di database.  
  
 L'annotazione **sql:use-cdata** accetta un valore booleano (0 , false, 1 , true). I valori possibili sono 0, 1, true e false.  
  
 Questa annotazione non può essere utilizzata con i tipi di attributo **sql:url-encode** o nei tipi di attributo ID, IDREF, IDREFS, NMTOKEN e NMTOKENS.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per ulteriori informazioni, vedere [Requisiti per l'esecuzione di esempi SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>R. Specifica di sql:use-cdata su un elemento  
 Nello schema seguente, **sql:use-cdata** è impostato su 1 (True) per il ** \<>AddressLine1** all'interno dell'elemento ** \<Address>.** I dati vengono quindi restituiti in una sezione CDATA.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Per testare una query Xpath di esempio sullo schema  
  
1.  Copiare il codice dello schema precedente e incollarlo in un file di testo. Salvare il file con il nome UseCData.xml.  
  
2.  Copiare il modello seguente e incollarlo in un file di testo. Salvare il file con il nome UseCDataT.xml nella stessa directory nella quale è stato salvato UseCData.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso della directory specificato per lo schema di mapping (UseCData.xml) è relativo alla directory nella quale viene salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per ulteriori informazioni, vedere [Utilizzo di ADO per l'esecuzione di query SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato il set di risultati parziale:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
