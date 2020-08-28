---
description: Ricezione di più recordset
title: Ricezione di più recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: abac183f348553f30bf0cf5ed91725ef421afb3e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979972"
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
