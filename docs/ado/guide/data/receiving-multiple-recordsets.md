---
title: Ricezione di più recordset | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 12aa80b918d11dad07119a26da3da8f27ef82cdb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759107"
---
# <a name="receiving-multiple-recordsets"></a>Ricezione di più recordset
Il [provider Microsoft OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) supporta la restituzione di più oggetti **Recordset** per un unico comando contenente più istruzioni SQL, un **Recordset** per ogni istruzione SQL. L'ordine in cui vengono restituiti i **Recordset**segue l'ordine in cui le istruzioni SQL vengono inserite nel testo del comando.  
  
 Il provider di OLE DB Microsoft per SQL Server restituisce inoltre più set di risultati a ADO quando il comando contiene una clausola COMPUTE. Ad esempio, un comando che contiene l'istruzione SQL seguente restituirà i risultati in due oggetti **Recordset** : uno per il set di righe di (*ProductID*, *ProductName*, *PrezzoUnitario*) e l'altro per il prezzo medio di tutti i prodotti nella tabella.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 È possibile utilizzare il metodo **Recordset. NextRecordset** per enumerare i due oggetti.  
  
 Per ulteriori informazioni, vedere [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
