---
title: Specifica di operatori booleani nelle query XPath (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath operators [SQLXML]
- OR operator
- Boolean operators
- XPath queries [SQLXML], Boolean operators
- operators [SQLXML]
ms.assetid: 9928cff5-62ac-42aa-96bf-2e09a1df0bc3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae0350a239414b4e20299cf42d46ebc5b9a69023
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273354"
---
# <a name="specifying-boolean-operators-in-xpath-queries-sqlxml-40"></a>Specifica di operatori booleani in query XPath (SQLXML 4.0)
  Negli esempi seguenti viene illustrato come specificare operatori booleani in query XPath. Le query XPath di questi esempi vengono specificate sullo schema di mapping contenuto in SampleSchema1.xml. Per informazioni su questo schema di esempio, vedere [Schema XSD con annotazioni di esempio per gli esempi XPath &#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-specify-the-or-boolean-operator"></a>A. Specificare l'operatore booleano OR  
 Questa query XPath restituisce il  **\<cliente >** figli del nodo di contesto con il **CustomerID** attributo pari a 13 o 31:  
  
```  
/child::Customer[attribute::CustomerID="13" or attribute::CustomerID="31"]  
```  
  
 È possibile specificare un collegamento all'asse `attribute` (@) e, poiché l'asse `child` è l'asse predefinito, può essere omesso dalla query:  
  
```  
/Customer[@CustomerID="13" or @CustomerID="31"]  
```  
  
 Nel predicato `attribute` è l'asse e `CustomerID` è il test di nodo (TRUE se **CustomerID** è un  **\<attributo >** nodo, in quanto il  **\<attributo >** nodo è il nodo primario per il `attribute` asse). Il predicato filtra le  **\<cliente >** elementi e restituisce solo quelli che soddisfano le condizioni specificate nel predicato.  
  
##### <a name="to-test-the-xpath-queries-against-the-mapping-schema"></a>Per testare query Xpath sullo schema di mapping  
  
1.  Copia il [esempi di codice schema](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md) e incollarlo in un file di testo. Salvare il file con il nome SampleSchema1.xml.  
  
2.  Creare il modello seguente (BooleanOperatorsA.xml) e salvarlo nella directory in cui è stato salvato il file SampleSchema1.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="13" or @CustomerID="31"]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Il percorso di directory specificato per lo schema di mapping SampleSchema1.xml è relativo alla directory in cui è salvato il modello. È possibile specificare anche un percorso assoluto, ad esempio:  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  Creare e utilizzare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) per eseguire il modello.  
  
     Per altre informazioni, vedere [utilizzo di ADO per eseguire query di SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Di seguito è riportato il set di risultati relativo all'esecuzione del modello:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="31" SalesPersonID="286" TerritoryID="7" AccountNumber="31" CustomerType="S" Orders="Ord-51803 Ord-69427">  
    <Order SalesOrderID="Ord-51803" SalesPersonID="286" OrderDate="2003-08-01T00:00:00" DueDate="2003-08-13T00:00:00" ShipDate="2003-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-718" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-838" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    <Order SalesOrderID="Ord-69427" SalesPersonID="286" OrderDate="2004-05-01T00:00:00" DueDate="2004-05-13T00:00:00" ShipDate="2004-05-08T00:00:00">  
      <OrderDetail ProductID="Prod-835" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
  </Customer>  
</ROOT>  
```  
  
  
