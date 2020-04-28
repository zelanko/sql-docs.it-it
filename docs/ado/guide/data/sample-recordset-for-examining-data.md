---
title: Recordset di esempio per l'analisi dei dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1882c5298d92e17a7ddaa165288fddfab7fdb02b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924300"
---
# <a name="sample-recordset-for-examining-data"></a>Recordset di esempio per l'esame dei dati
Per prima cosa, esaminiamo l'oggetto **Recordset** come restituito usando la query SQL seguente, eseguita sul database di esempio Northwind in Microsoft SQL Server.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 L'oggetto **Recordset** risultante contiene tutti i prodotti nel database indicati nella tabella seguente.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Pere organiche secche di zio Bob|30,0000|  
|14|Tofu|23,2500|  
|28|Crauti Rssle|45,6000|  
|51|Mele Manjimup secche|53,0000|  
|74|Tofu Longlife|10,0000|  
  
 Se si è interessati a ottenere questi risultati, provare l'esempio JScript seguente:  
  
-   [Esempio di JScript per la restituzione di un recordset](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
