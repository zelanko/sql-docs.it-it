---
description: Proprietà Ordinal (Position - ADO MD)
title: Proprietà ordinale (posizione ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: c2f145cf96222eb08ab154dc9d683c0973cad861
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777920"
---
# <a name="ordinal-property-ado-md-position"></a>Proprietà Ordinal (Position - ADO MD)
Identifica in modo univoco una [posizione](./position-object-ado-md.md) lungo un asse.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 La proprietà **ordinale** di un oggetto [position](./position-object-ado-md.md) corrisponde all'indice della **posizione** all'interno dell' [insieme Positions](./positions-collection-ado-md.md) .  
  
 È possibile recuperare rapidamente una cella utilizzando il **numero ordinale** della **posizione** lungo ogni asse con la proprietà [Item](./item-property-ado-md-cellset.md) dell'oggetto [cellt](./cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Position (ADO MD)](./position-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto cellt (ADO MD)](./cellset-object-ado-md.md)   
 [Proprietà Item (ADO MD Cellt)](./item-property-ado-md-cellset.md)   
 [Proprietà Ordinal (Cell - ADO MD)](./ordinal-property-ado-md-cell.md)