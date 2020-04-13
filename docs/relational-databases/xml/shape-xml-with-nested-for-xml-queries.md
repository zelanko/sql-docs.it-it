---
title: Determinare la struttura dei valori XML tramite query FOR XML annidate | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d3e3b9e0636e9164e5be3181ee2a24070fc4323
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664998"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>Determinare la struttura dei valori XML tramite query nidificate FOR XML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Nell'esempio seguente viene eseguita una query sulla tabella `Production.Product` per recuperare i valori di `ListPrice` e `StandardCost` di un prodotto specifico. Per rendere la query più interessante, entrambi i prezzi vengono restituiti in un elemento <`Price`> e ogni elemento <`Price`> include un attributo `PriceType`.  
  
## <a name="example"></a>Esempio  
 La struttura prevista del valore XML è la seguente:  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 La query FOR XML nidificata è la seguente:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 Dalla query precedente si noti quanto segue:  
  
-   L'istruzione SELECT esterna costruisce l'elemento <`Product`>, che ha un attributo **ProductID** e due elementi <`Price`> figlio.  
  
-   Le due istruzioni SELECT interne costruiscono due elementi <`Price`>, ognuno con un attributo **PriceType** e un valore XML che restituisce il prezzo del prodotto.  
  
-   La direttiva XMLSCHEMA nell'istruzione SELECT più esterna genera lo schema XSD inline che descrive la struttura del valore XML risultante.  
  
 Per rendere la query più interessante, è possibile creare la query FOR XML e quindi creare una query XQuery sul risultato in modo da modificare la struttura del valore XML, come illustrato nella query seguente:  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 L'esempio precedente usa il metodo **query()** con tipo di dati **xml** per eseguire una query sul valore XML restituito dalla query FOR XML interna e costruire il risultato previsto.  
  
 Risultato:  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di query FOR XML nidificate](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
