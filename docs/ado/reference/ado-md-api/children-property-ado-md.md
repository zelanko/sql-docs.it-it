---
title: Proprietà Children (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 219aeba8cfc7e913a2febdd031c844aed922832e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709668"
---
# <a name="children-property-ado-md"></a>Proprietà Children (ADO MD)
Restituisce un [membri](../../../ado/reference/ado-md-api/members-collection-ado-md.md) raccolta per cui corrente [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) padre nella gerarchia.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **membri** raccolta ed è di sola lettura.  
  
## <a name="remarks"></a>Note  
 Il **figli** proprietà contiene un **membri** raccolta per cui corrente **membro** è l'oggetto padre gerarchico. A livello di foglia **membro** gli oggetti non presentano membri figlio **membri** raccolta. Questa proprietà è supportata solo nei **membro** oggetti appartenenti a un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto. Si verifica un errore quando questa proprietà viene fatto riferimento dal **membro** oggetti appartenenti a un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) oggetto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
