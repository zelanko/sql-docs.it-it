---
title: Recordset di esempio per analisi dei dati | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924300"
---
# <a name="sample-recordset-for-examining-data"></a>Recordset di esempio per l'esame dei dati
In primo luogo, verrà ora esaminato il **Recordset** dell'oggetto restituito utilizzando la seguente query SQL, eseguita su base in Microsoft SQL Server i dati di esempio Northwind.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 I risultanti **Recordset** oggetto contiene tutte le produce nel database indicato nella tabella seguente.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Secca biologica frutta|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle rossi|45.6000|  
|51|Manjimup secchi mele|53.0000|  
|74|Tofu a lunga conservazione|10.0000|  
  
 Se si desidera ricevere tali risultati manualmente, provare l'esempio JScript seguente:  
  
-   [Esempio di JScript per restituire un Recordset](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
