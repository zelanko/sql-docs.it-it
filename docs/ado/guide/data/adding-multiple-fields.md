---
description: Aggiunta di più campi e valori
title: Aggiunta di più campi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c661e8e99ae9651a4b89f8facad238d5f83564e9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991772"
---
# <a name="adding-multiple-fields-and-values"></a>Aggiunta di più campi e valori
Occasionalmente, potrebbe essere più efficiente passare una matrice di campi e i relativi valori corrispondenti al metodo **AddNew** , anziché impostare il **valore** più volte per ogni nuovo campo. Se *FieldName* è una matrice, *i valori* devono essere anche una matrice con lo stesso numero di membri. in caso contrario, si verifica un errore. L'ordine dei nomi di campo deve corrispondere all'ordine dei valori di campo in ogni matrice. Il codice seguente passa una matrice di campi e una matrice di valori al metodo **AddNew** .

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
