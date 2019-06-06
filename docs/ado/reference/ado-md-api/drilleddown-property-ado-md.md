---
title: Proprietà DrilledDown (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 83db7cfc6cac6dde34ca8d2a974c9d926ba9f086
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709442"
---
# <a name="drilleddown-property-ado-md"></a>Proprietà DrilledDown (ADO MD)
Indica se gli elementi figlio seguono immediatamente il [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) sull'asse.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **booleana** valore ed è di sola lettura. **DrilledDown** restituisce **True** se non esistono membri figlio del membro corrente sull'asse. **DrilledDown** restituisce **False** se il membro corrente ha uno o più membri figlio sull'asse.  
  
## <a name="remarks"></a>Note  
 Usare la **DrilledDown** proprietà per determinare se è presente almeno un figlio di questo membro sull'asse immediatamente dopo questo membro. Queste informazioni sono utili quando si visualizza il membro.  
  
 Questa proprietà è supportata solo nei [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetti appartenenti a un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) oggetto. Si verifica un errore quando questa proprietà viene fatto riferimento dal **membro** oggetti appartenenti a un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ParentSameAsPrev (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
