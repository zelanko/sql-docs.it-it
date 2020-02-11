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
ms.openlocfilehash: cbec9733044127d23e75364697a41ccd7e8910e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911526"
---
# <a name="children-property-ado-md"></a>Proprietà Children (ADO MD)
Restituisce una raccolta di [membri](../../../ado/reference/ado-md-api/members-collection-ado-md.md) per cui il [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) corrente è l'elemento padre nella gerarchia.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una raccolta di **membri** ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **Children** contiene una raccolta di **membri** per cui il **membro** corrente è l'elemento padre gerarchico. Gli oggetti **membro** a livello foglia non hanno membri figlio nella raccolta **Members** . Questa proprietà è supportata solo per gli oggetti **membro** che appartengono a un oggetto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Si verifica un errore quando si fa riferimento a questa proprietà dagli oggetti **membro** che appartengono a un oggetto [position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ChildCount (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
