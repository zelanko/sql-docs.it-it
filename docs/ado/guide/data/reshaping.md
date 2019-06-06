---
title: Modifica della forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d7137d67c14cd435ffe814a3bfbf0e42a7be976
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700422"
---
# <a name="reshaping"></a>Modifica della forma
Oggetto **Recordset** creato da una clausola di una forma comando può essere assegnato un *alias* nome (in genere con la parola chiave AS). L'alias di una data shaping **Recordset** possibile farvi riferimento in un comando di completamente diverso. Vale a dire, è possibile riutilizzare, oppure *reshape*, una forma precedentemente **Recordset** in un nuovo comando di forma. Per supportare questa funzionalità, ADO fornisce una proprietà, [Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 Modificare la forma ha due funzioni principali. Il primo consiste nell'associare un oggetto esistente **Recordset** con un nuovo elemento padre **Recordset**.  
  
## <a name="example"></a>Esempio  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 La seconda funzione viene per abilitare l'accesso non faceva parte di un elemento figlio esistente **Recordset** oggetti, usando la sintassi "forma \<recordset proprietà dinamica reshape name >".  
  
> [!NOTE]
>  Non è possibile aggiungere colonne a un oggetto esistente **Recordset**, modificare la forma un con parametri **Recordset** o nella **Recordset** gli oggetti in una clausola COMPUTE interessata oppure eseguire operazioni su una qualsiasi di aggregazione **Recordset** discendente dalle **Recordset** quest'ultimo. Il **Recordset** quest'ultimo e la nuova forma comando devono usare lo stesso [connessione](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)
