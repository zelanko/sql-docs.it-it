---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d29618fbacfbd4ba3becd222ef8a063e59e2cc70
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697838"
---
# <a name="getchildren-method-ado"></a>Metodo GetChildren (ADO)
Restituisce un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) contenente le righe rappresentano gli elementi figlio di una raccolta [Record](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **Recordset** oggetto per cui ogni riga rappresenta un elemento figlio dell'oggetto corrente **Record** oggetto. Ad esempio, gli elementi figlio di un **Record** che rappresenta una directory sarebbero i file e sottodirectory contenute all'interno della directory padre.  
  
## <a name="remarks"></a>Note  
 Il provider determina quali colonne sono presenti nell'oggetto restituito **Recordset**. Ad esempio, un provider di origine del documento restituisce sempre una risorsa **Recordset**.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|
