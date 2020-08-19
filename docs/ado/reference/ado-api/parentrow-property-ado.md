---
description: Proprietà ParentRow (ADO)
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
ms.openlocfilehash: b81fc704c78b620c1319aa592336aba0489a3d37
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442743"
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
