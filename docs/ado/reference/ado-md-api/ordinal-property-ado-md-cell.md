---
title: Proprietà Ordinal (Cell-ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 194b72ce66eb2efdc3a246f24948b01c790f7b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949372"
---
# <a name="ordinal-property-ado-md-cell"></a>Proprietà Ordinal (Cell - ADO MD)
Identifica in modo univoco un [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md) in base alla posizione all'interno di un set di celle.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **lungo** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Note  
 Valore ordinale della cella identifica in modo univoco la cella all'interno di un set di celle. Concettualmente, le celle sono numerate in un set di celle come se fosse il set di celle un' *p*-matrice dimensionale, dove *p* è il numero di [assi](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Le celle sono numerate a partire da zero in ordine di riga. Ecco la formula per calcolare il numero ordinale di una cella:  
  
 Valore ordinale della cella può essere utilizzato con il [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) proprietà del [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto per recuperare rapidamente i [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Proprietà Item (Cellset-ADO MD)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Proprietà Ordinal (Position - ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
