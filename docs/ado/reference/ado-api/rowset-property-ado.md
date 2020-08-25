---
description: Proprietà Rowset (ADO)
title: Proprietà Rowset (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f966261864cb7717b31e4851062228c3e6d63e92
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777620"
---
# <a name="rowset-property-ado"></a>Proprietà Rowset (ADO)
Ottiene o imposta un oggetto OLE DB **set di righe** da/in un oggetto **ADORecordsetConstruction** . Quando si utilizza put_Rowset, il set di righe viene trasformato in un oggetto **Recordset** ADO.  
  
 Proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRowset*  
 Puntatore a un oggetto **set di righe** OLE DB.  
  
 *PRowset*  
 Oggetto **set di righe** OLE DB.  
  
## <a name="return-values"></a>Valori restituiti  
 Questo metodo di proprietà restituisce i valori HRESULT standard, inclusi S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordsetConstruction](./adorecordsetconstruction-interface.md)