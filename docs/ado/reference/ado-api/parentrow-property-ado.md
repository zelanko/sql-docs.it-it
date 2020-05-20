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
author: rothja
ms.author: jroth
ms.openlocfilehash: 54d89c536145f413513fa67a8e76f7f00cf8322c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763372"
---
# <a name="parentrow-property-ado"></a>Proprietà ParentRow (ADO)
Imposta il contenitore di un oggetto OLE DB **riga** su un oggetto **ADORecordConstruction** , in modo che l'elemento padre della riga venga trasformato in un oggetto **record** ADO.  
  
 Sola scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parametri  
 *pParent*  
 Contenitore di una riga.  
  
## <a name="return-values"></a>Valori restituiti  
 Questo metodo di proprietà restituisce i valori HRESULT standard, inclusi S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
