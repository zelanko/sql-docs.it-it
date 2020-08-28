---
description: Proprietà State (ADO MD)
title: Proprietà state (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: rothja
ms.author: jroth
ms.openlocfilehash: 78b96e242cc27d27326d97f51cf378d9c5cbb51e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985982"
---
# <a name="state-property-ado-md"></a>Proprietà State (ADO MD)
Indica lo stato corrente del cellt.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer che indica la condizione corrente dell'oggetto [cellt](./cellset-object-ado-md.md) ed è di sola lettura. I valori seguenti sono validi: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Osservazioni  
 Per utilizzare i nomi delle costanti [ObjectStateEnum](../ado-api/objectstateenum.md) , è necessario che nel progetto sia presente la libreria dei tipi ADO a cui si fa riferimento. Per ulteriori informazioni, vedere [utilizzo di ADO con ADO MD](../../guide/multidimensional/using-ado-with-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Close (ADO MD)](./close-method-ado-md.md)   
 [Metodo Open (ADO MD)](./open-method-ado-md.md)