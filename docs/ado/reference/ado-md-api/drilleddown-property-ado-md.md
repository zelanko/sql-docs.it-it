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
ms.openlocfilehash: f1175d2a70c376e3da1e079e4a3eb93a39235758
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938465"
---
# <a name="drilleddown-property-ado-md"></a>Proprietà DrilledDown (ADO MD)
Indica se gli elementi figlio seguono immediatamente il [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) sull'asse.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **booleano** ed è di sola lettura. **DrilledDown** restituisce **true** se non sono presenti membri figlio del membro corrente sull'asse. **DrilledDown** restituisce **false** se il membro corrente ha uno o più membri figlio sull'asse.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **DrilledDown** per determinare se è presente almeno un elemento figlio di questo membro sull'asse immediatamente successivo a questo membro. Queste informazioni sono utili per la visualizzazione del membro.  
  
 Questa proprietà è supportata solo per gli oggetti [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) che appartengono a un oggetto [position](../../../ado/reference/ado-md-api/position-object-ado-md.md) . Si verifica un errore quando si fa riferimento a questa proprietà dagli oggetti **membro** che appartengono a un oggetto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ParentSameAsPrev (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
