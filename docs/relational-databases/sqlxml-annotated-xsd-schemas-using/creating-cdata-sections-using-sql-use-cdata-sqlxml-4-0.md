---
title: 'Creazione di sezioni CDATA mediante SQL: use-cdata (SQLXML 4.0) | Documenti di Microsoft'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9b7cac79155e89217a64fbbc309082322853f80
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041592"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Creazione di sezioni CDATA mediante sql:use-cdata (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In XML vengono utilizzate le sezioni CDATA per eseguire l'escape di blocchi di testo contenenti caratteri che, altrimenti, verrebbero riconosciuti come caratteri di markup.  
  
 Un database in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] talvolta può contenere caratteri considerati caratteri di markup dal parser XML, ad esempio le parentesi angolari (< e >), il simbolo minore di o uguale a (<=) e l'e commerciale (&). Per evitare che ciò accada, è tuttavia possibile eseguire il wrapping di questo tipo di caratteri speciali in una sezione CDATA. Il testo nella sezione CDATA viene considerato testo normale dal parser XML.  
  
 Il **SQL: use-cdata** annotazione viene usata per specificare che i dati restituiti dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere incapsulate in una sezione CDATA (vale a dire, indica se il valore da una colonna che è specificato da **SQL: field** deve essere incluso in una sezione CDATA). Il **SQL: use-cdata** annotazione può essere specificata solo su elementi che eseguono il mapping a una colonna di database.  
  
 Il **SQL: use-cdata** annotazione accetta un valore booleano (0 = false, 1 = true). I valori possibili sono 0, 1, true e false.  
  
 Questa annotazione non può essere utilizzata con **SQL: url-encode** o sull'ID, IDREF, IDREFS, NMTOKEN e NMTOKENS tipi di attributo.  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare alcuni requisiti. Per altre informazioni, vedere [requisiti per l'esecuzione di esempi di SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. Specifica di sql:use-cdata su un elemento  
 Nello schema seguente, **SQL: use-cdata** è impostata su 1 (True) per il  **\<AddressLine1 >** all'interno di  **\<indirizzo >** elemento. I dati vengono quindi restituiti in una sezione CDATA.  
  
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
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
