---
title: Proprietà ParentRow (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ea31baf4b215a6a516c13b438b526b8e9d8b612
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027881"
---
# <a name="parentrow-property-ado"></a>Proprietà ParentRow (ADO)
Imposta il contenitore di OLE DB **riga** dell'oggetto in un **ADORecordConstruction** dell'oggetto, in modo che l'elemento padre della riga viene trasformato in un oggetto ADO **Record** oggetto.  
  
 Sola scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parametri  
 *pParent*  
 Un contenitore di una riga.  
  
## <a name="return-values"></a>Valori restituiti  
 Metodo di questa proprietà restituisce i valori HRESULT standard, tra cui S_OK ed E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
