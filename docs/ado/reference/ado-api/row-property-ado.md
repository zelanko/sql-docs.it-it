---
title: Proprietà (ADO) di riga | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 041356f05daaaef50e6e81d995209ab5379fc901
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192829"
---
# <a name="row-property-ado"></a>Proprietà Row (ADO)
Ottiene o imposta un DB OLE **riga** oggetto da o in un [interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md) oggetto. Quando si usa **put_Row** per impostare un **riga** dell'oggetto, una riga viene trasformata in un oggetto ADO **Record** oggetto.  
  
## <a name="readwritesyntax"></a>Lettura/scrittura. Sintassi  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parametri  
 *ppRow*  
 Puntatore a OLE DB **riga** oggetto.  
  
 *PRow*  
 OLE DB **riga** oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Metodo di questa proprietà restituisce i valori HRESULT standard, tra cui S_OK ed E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
