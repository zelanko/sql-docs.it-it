---
title: Proprietà state (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c11bb74b62d54b1e2489cba5dd7cd35ee376a41
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949151"
---
# <a name="state-property-ado-md"></a>Proprietà State (ADO MD)
Indica lo stato corrente del cellt.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer che indica la condizione corrente dell'oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) ed è di sola lettura. I valori seguenti sono validi: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Osservazioni  
 Per utilizzare i nomi delle costanti [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) , è necessario che nel progetto sia presente la libreria dei tipi ADO a cui si fa riferimento. Per ulteriori informazioni, vedere [utilizzo di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Metodo Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
