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
manager: jroth
ms.openlocfilehash: 9ffc34dd95ac2f5ef6e26e796c4c05cd91b28ae0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700394"
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
