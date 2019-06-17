---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fad2ee85ef40431a6a4e16814f4711404c851d3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711454"
---
# <a name="rowposition-property-ado"></a>Proprietà RowPosition (ADO)
Ottiene o imposta un DB OLE **RowPosition** oggetto da/in un **ADORecordsetConstruction** oggetto. Quando si usa **put_RowPosition** per impostare il **RowPosition** oggetto, risultante **Recordset** oggetto utilizza il **RowPosition** dell'oggetto a determinare la riga corrente.  
  
 Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRowPos*  
 Puntatore a OLE DB **RowPosition** oggetto.  
  
 *PRowPos*  
 OLE DB **RowPosition** oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Metodo di questa proprietà restituisce i valori HRESULT standard, tra cui S_OK ed E_FAIL.  
  
## <a name="remarks"></a>Note  
 Quando questa proprietà è impostata, se il **set di righe** dell'oggetto nel **RowPosition** oggetto è diverso dal **set di righe** dell'oggetto nel **Recordset**dell'oggetto, il primo esegue l'override di quest'ultimo. Lo stesso comportamento si applica all'oggetto corrente **capitolo** delle **RowPosition** anche.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
