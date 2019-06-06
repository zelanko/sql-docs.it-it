---
title: Ricezione di recordset multipli | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 78e6ed78e8c61a9ce14e30f0eb286d55da0e63b9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700742"
---
# <a name="receiving-multiple-recordsets"></a>Ricezione di più recordset
Il [Provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) supporta la restituzione dei più **Recordset** oggetti per un unico comando che contiene più istruzioni SQL, uno **Recordset**per ogni istruzione SQL. L'ordine in cui il **Recordset**verranno restituiti segue l'ordine in cui le istruzioni SQL vengono inserite nel testo del comando.  
  
 Il Provider Microsoft OLE DB per SQL Server anche restituisce più set di risultati di ADO quando il comando contiene una clausola COMPUTE. Ad esempio, un comando che contiene l'istruzione SQL seguente restituirà i risultati in due **Recordset** oggetti: una per il set di righe di (*ProductID*, *ProductName*, *UnitPrice*) e l'altro per il prezzo medio di tutti i prodotti nella tabella.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 È possibile usare la **NextRecordset** metodo per enumerare i due oggetti.  
  
 Per altre informazioni, vedere [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
