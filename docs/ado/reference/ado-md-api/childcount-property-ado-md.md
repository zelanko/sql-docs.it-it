---
title: Proprietà ChildCount (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: rothja
ms.author: jroth
ms.openlocfilehash: 858bed2c2fe04a1fbf0486b0e0bfc9a26447e4ef
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764402"
---
# <a name="childcount-property-ado-md"></a>Proprietà ChildCount (ADO MD)
Indica il numero di membri per i quali l'oggetto [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) corrente è l'elemento padre in una gerarchia.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare la proprietà **childCount** per restituire una stima del numero di elementi figlio di un **membro** . Gli elementi figlio effettivi di un **membro** possono essere restituiti dalla proprietà [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
 Per gli oggetti **membro** di un oggetto [position](../../../ado/reference/ado-md-api/position-object-ado-md.md) , il numero massimo restituito è 65536. Se il numero effettivo di elementi figlio supera 65536, il valore restituito sarà comunque 65536. Pertanto, l'applicazione deve interpretare un **childCount** di 65536 come uguale o maggiore di 65536 figli.  
  
 Per gli oggetti **membro** di un oggetto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) , utilizzare la proprietà [conteggio](../../../ado/reference/ado-api/count-property-ado.md) raccolta ADO nella raccolta **Children** per determinare il numero esatto di elementi figlio. La determinazione del numero esatto di elementi figlio può essere lenta se il numero di elementi figlio nella raccolta è elevato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Proprietà Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
