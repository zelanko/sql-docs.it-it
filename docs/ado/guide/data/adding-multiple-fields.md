---
title: Aggiunta di più campi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 07a1a3723b4169872c1b8aa872457e67a60d1f71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926270"
---
# <a name="adding-multiple-fields-and-values"></a>Aggiunta di più campi e valori
In alcuni casi, potrebbe essere più efficiente per passare una matrice di campi e i relativi valori per il **AddNew** metodo, anziché l'impostazione **valore** più volte per ogni nuovo campo. Se *FieldList* è una matrice *valori* deve anche essere una matrice con lo stesso numero di membri; in caso contrario, si verifica un errore. L'ordine dei nomi di campo deve corrispondere all'ordine dei valori di campo in ogni matrice. Il codice seguente passa una matrice di campi e una matrice di valori per il **AddNew** (metodo).

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```
