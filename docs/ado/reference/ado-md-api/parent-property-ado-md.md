---
title: Proprietà (ADO MD) padre | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cb0b93ba1be2570ecd474ed1244bec16575180d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156259"
---
# <a name="parent-property-ado-md"></a>Proprietà Parent (ADO MD)
Indica il membro padre dell'oggetto corrente [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) in una gerarchia.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetto ed è di sola lettura.  
  
## <a name="remarks"></a>Note  
 Un membro al livello superiore di una gerarchia (radice) non ha elementi padre. Questa proprietà è supportata solo sugli **membro** oggetti appartenenti a un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto. Si verifica un errore quando questa proprietà viene fatto riferimento dal **membro** oggetti appartenenti a un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
