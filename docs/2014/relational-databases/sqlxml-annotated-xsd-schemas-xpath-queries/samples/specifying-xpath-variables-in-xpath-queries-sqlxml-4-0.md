---
title: Specifica di variabili XPath in query XPath (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], XPath variables
- XPath variables [SQLXML]
ms.assetid: c11ab816-11b8-4131-8b77-c03fe500fa10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25e6c96ccbe51ccc0d2d88c4b119c08538d37fcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010689"
---
# <a name="specifying-xpath-variables-in-xpath-queries-sqlxml-40"></a>Definizione di variabili XPath in query XPath (SQLXML 4.0)
  Negli esempi seguenti viene illustrato il modo in cui passare variabili XPath in query XPath. Le query XPath di questi esempi vengono specificate sullo schema di mapping contenuto in SampleSchema1.xml. Per informazioni su questo schema di esempio, vedere [schema XSD con annotazioni di esempio per gli esempi XPath &#40;SQLXML 4,0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-use-the-xpath-variables"></a>R. Utilizzare le variabili XPath  
 Un modello di esempio è costituito da due query XPath. Ognuna delle query XPath accetta un parametro. Il modello specifica inoltre valori predefiniti per tali parametri. Se i valori dei parametri non sono specificati, vengono utilizzati i valori predefiniti. In ** \<SQL: header>** vengono specificati due parametri con valori predefiniti.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:header>  
     <sql:param name='CustomerID'>1</sql:param>  
     <sql:param name='ContactID'>1</sql:param>   
  </sql:header>  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
    Customer[@CustomerID=$CustomerID]   
  </sql:xpath-query >  
  <sql:xpath-query mapping-schema="SampleSchema1.xml">  
   Contact[@ContactID=$ContactID]   
  </sql:xpath-query>  
</ROOT>  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copiare il [codice dello schema di esempio](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello seguente (XPathVariables.xml) e salvarlo nella directory in cui:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:header>  
         <sql:param name='CustomerID'>1</sql:param>  
         <sql:param name='ContactID'>1</sql:param>   
      </sql:header>  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[@CustomerID=$CustomerID]   
      </sql:xpath-query >  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
       Contact[@ContactID=$ContactID]   
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello. Per ulteriori informazioni, vedere [utilizzo di ADO per eseguire query SQLXML 4,0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
> [!NOTE]  
>  In questo esempio non viene passato alcun parametro. Vengono pertanto utilizzati i valori di parametro predefiniti.  
  
  
