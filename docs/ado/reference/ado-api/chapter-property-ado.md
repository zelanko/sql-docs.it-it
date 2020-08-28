---
description: Proprietà Chapter (ADO)
title: Proprietà Chapter (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: rothja
ms.author: jroth
ms.openlocfilehash: ea7810e7b829991d185edf49f8224db57535f947
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975522"
---
# <a name="chapter-property-ado"></a>Proprietà Chapter (ADO)
Ottiene o imposta un oggetto OLE DB **capitolo** da/in un oggetto di [Interfaccia ADORecordsetConstruction](./adorecordsetconstruction-interface.md) . Quando si utilizza **put_Chapter** per impostare l'oggetto **capitolo** , un subset di righe viene trasformato in un oggetto [oggetto recordset](./recordset-object-ado.md) ADO. Viene impostato il capitolo corrente dell'oggetto **set di righe**. Si tratta di una proprietà di lettura/scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>Parametri  
 *plChapter*  
 Puntatore all'handle di un capitolo.  
  
 *LChapter*  
 Handle di un capitolo.  
  
## <a name="return-values"></a>Valori restituiti  
 Questo metodo di proprietà restituisce i valori HRESULT standard, inclusi S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia ADORecordsetConstruction](./adorecordsetconstruction-interface.md)