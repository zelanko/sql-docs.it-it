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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8e6f6a7cb749ff2b22a1f7563b43ce07e060aab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911550"
---
# <a name="childcount-property-ado-md"></a>Proprietà ChildCount (ADO MD)
Indica il numero di membri per il quale l'oggetto corrente [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetto è il padre in una gerarchia.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **lungo** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Note  
 Usare la **ChildCount** proprietà per restituire una stima del numero di figli di un **membro** ha. Gli elementi figlio effettivi di una **membro** possono essere restituiti dai [figli](../../../ado/reference/ado-md-api/children-property-ado-md.md) proprietà.  
  
 Per la **membro** oggetti da un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) dell'oggetto, il numero massimo restituito è 65536. Se il numero effettivo di elementi figlio supera i 65536, il valore restituito sarà ancora 65536. Pertanto, deve interpretare l'applicazione un' **ChildCount** di 65536 come uguale o maggiore di 65536 figli.  
  
 Per **membro** oggetti da un [a livello di](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto, usare la raccolta di ADO [Count](../../../ado/reference/ado-api/count-property-ado.md) proprietà il **figli** insieme per determinare il numero esatto di elementi figlio. Determinare il numero esatto di elementi figlio può essere lenta se il numero di elementi figlio nella raccolta è di grandi dimensioni.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Proprietà Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
