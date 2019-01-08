---
title: Specifica di funzioni booleane in query XPath (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], Boolean functions
- false function
- not function [SQLXML]
- true function
- Boolean functions
ms.assetid: c72cd333-9294-4d41-84f2-1748bf20e3eb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f31498e5b73ce639808df6c659250a4ba6268308
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749993"
---
# <a name="specifying-boolean-functions-in-xpath-queries-sqlxml-40"></a>Definizione di funzioni booleane in query XPath (SQLXML 4.0)
  Negli esempi seguenti viene illustrato come specificare funzioni booleane in query XPath. Le query XPath di questi esempi vengono specificate sullo schema di mapping contenuto in SampleSchema1.xml. Per informazioni su questo schema di esempio, vedere [Schema XSD con annotazioni di esempio per gli esempi XPath &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Esempi  
  
## <a name="a-specify-the-not-boolean-function"></a>A. Definizione della funzione booleana not()  
 Questa query restituisce tutti i  **\<cliente >** elementi figlio del nodo di contesto che non hanno  **\<ordine >** gli elementi figlio:  
  
```  
/child::Customer[not(child::Order)]  
```  
  
 L'asse `child` è l'asse predefinito. È pertanto possibile specificare la query nel modo seguente:  
  
```  
/Customer[not(Order)]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copia il [esempi di codice schema](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello seguente (BooleanFunctionsA.xml) e salvarlo nella directory in cui è stato salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        Customer[not(Order)]  
    </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito viene indicato il set di risultati parziale dell'esecuzione del modello:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
## <a name="b-specify-the-true-and-false-boolean-functions"></a>b. Definizione delle funzioni booleane true() e false()  
 Questa query restituisce tutte le  **\<cliente >** figli del nodo di contesto che non hanno  **\<ordine >** gli elementi figlio. In termini relazionali, questa query restituisce tutti i clienti che non hanno effettuato ordini.  
  
```  
/child::Customer[child::Order=false()]  
```  
  
 L'asse `child` è l'asse predefinito. È pertanto possibile specificare la query nel modo seguente:  
  
```  
/Customer[Order=false()]  
```  
  
 La query equivale a quanto segue:  
  
```  
/Customer[not(Order)]  
```  
  
 Nella query seguente vengono restituiti tutti i clienti che hanno effettuato almeno un ordine:  
  
```  
/Customer[Order=true()]  
```  
  
 La query equivale a quanto segue:  
  
```  
/Customer[Order]  
```  
  
#### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>Per testare la query Xpath sullo schema di mapping  
  
1.  Copia il [esempi di codice schema](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello seguente (BooleanFunctionsB.xml) e salvarlo nella directory in cui è stato salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[Order=false()]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito viene indicato il set di risultati parziale dell'esecuzione del modello:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="32" SalesPersonID="289" TerritoryID="8" AccountNumber="32" CustomerType="S" />   
  <Customer CustomerID="35" SalesPersonID="275" TerritoryID="2" AccountNumber="35" CustomerType="S" />   
  ...  
</ROOT>  
```  
  
  
