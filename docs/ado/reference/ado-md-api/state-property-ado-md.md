---
title: Stato proprietà (ADO MD) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949151"
---
# <a name="state-property-ado-md"></a>Proprietà State (ADO MD)
Indica lo stato corrente del set di celle.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **lungo** valore intero che indica la condizione corrente del [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto ed è di sola lettura. I valori seguenti sono validi: **adStateClosed** (0) e **adStateOpen** (1).  
  
## <a name="remarks"></a>Note  
 Usare la [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) i nomi delle costanti, è necessario disporre la raccolta di tipo ADO cui viene fatto riferimento nel progetto. Visualizzare [utilizzo di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) per altre informazioni.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Close (metodo) (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Metodo Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
