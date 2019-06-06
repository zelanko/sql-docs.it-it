---
title: Proprietà rowset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f528ef5c83f0a9922c32fb06955d0ff921bfae6c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711433"
---
# <a name="rowset-property-ado"></a>Proprietà Rowset (ADO)
Ottiene o imposta un DB OLE **Rowset** oggetto da/in un **ADORecordsetConstruction** oggetto. Quando si usa put_Rowset, il set di righe viene trasformato in un oggetto ADO **Recordset** oggetto.  
  
 Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRowset*  
 Puntatore a OLE DB **set di righe** oggetto.  
  
 *PRowset*  
 OLE DB **set di righe** oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Metodo di questa proprietà restituisce i valori HRESULT standard, tra cui S_OK ed E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
