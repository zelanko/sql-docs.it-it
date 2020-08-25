---
description: Proprietà RowPosition (ADO)
title: Proprietà RowPosition (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f5f78843e38c2a3ff6b21c90bc9ed7f2c573ee4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777610"
---
# <a name="rowposition-property-ado"></a>Proprietà RowPosition (ADO)
Ottiene o imposta un OLE DB oggetto **RowPosition** da/in un oggetto **ADORecordsetConstruction** . Quando si utilizza **put_RowPosition** per impostare l'oggetto **RowPosition** , l'oggetto **Recordset** risultante utilizza l'oggetto **RowPosition** per determinare la riga corrente.  
  
 Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRowPos*  
 Puntatore a un oggetto OLE DB **RowPosition** .  
  
 *PRowPos*  
 Oggetto OLE DB **RowPosition** .  
  
## <a name="return-values"></a>Valori restituiti  
 Questo metodo di proprietà restituisce i valori HRESULT standard, inclusi S_OK e E_FAIL.  
  
## <a name="remarks"></a>Commenti  
 Quando questa proprietà è impostata, se l'oggetto **set di righe** nell'oggetto **RowPosition** è diverso dall'oggetto **set di righe** nell'oggetto **Recordset** , il primo esegue l'override di quest'ultimo. Lo stesso comportamento si applica anche al **capitolo** corrente di **RowPosition** .  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordsetConstruction](./adorecordsetconstruction-interface.md)