---
title: Creare viste su colonne XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d0e4798caf545c84f97cd05075d455980083bf4d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717081"
---
# <a name="create-views-over-xml-columns"></a>Creazione di viste
  Le colonne di tipo `xml` possono essere utilizzate per la creazione di viste. Nell'esempio seguente viene creata una vista nella quale il valore di una colonna di tipo `xml` viene recuperato utilizzando il metodo `value()` del tipo di dati `xml`.  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 Eseguire la query seguente sulla vista:  
  
```  
SELECT *   
FROM   MyView  
```  
  
 Risultato:  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 Notare i punti seguenti circa l'utilizzo del tipo di dati `xml` per creare viste:  
  
-   Il tipo di dati xml può essere creato in una vista materializzata. La vista materializzata non può essere basata su un metodo con tipo di dati XML, ma è possibile eseguirne il cast su una raccolta di XML Schema diversa dalla colonna di tipo xml nella tabella di base.  
  
-   Il tipo di dati `xml` non può essere utilizzato nelle viste partizionate distribuite.  
  
-   I predicati SQL in esecuzione sulla vista non saranno inseriti in XQuery per la definizione della vista.  
  
-   I metodi con tipo di dati XML in una vista non sono aggiornabili.  
  
  
