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
author: rothja
ms.author: jroth
ms.openlocfilehash: f0f712c6c1604f96d5d66d5ded712ae6efe54edb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760917"
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
