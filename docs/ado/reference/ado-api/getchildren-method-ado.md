---
description: Metodo GetChildren (ADO)
title: Metodo GetChildren (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
author: rothja
ms.author: jroth
ms.openlocfilehash: 906c20d19143f4f1e8fe0b6c1e91585893acfa5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443583"
---
# <a name="getchildren-method-ado"></a>Metodo GetChildren (ADO)
Restituisce un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) le cui righe rappresentano gli elementi figlio di un [record](../../../ado/reference/ado-api/record-object-ado.md)di raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **Recordset** per il quale ogni riga rappresenta un elemento figlio dell'oggetto **record** corrente. Ad esempio, gli elementi figlio di un **record** che rappresenta una directory sono i file e le sottodirectory contenuti nella directory padre.  
  
## <a name="remarks"></a>Osservazioni  
 Il provider determina le colonne presenti nel **Recordset**restituito. Un provider di origine del documento restituisce, ad esempio, sempre un **Recordset**di risorsa.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::
