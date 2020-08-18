---
description: Proprietà Ordinal (Cell - ADO MD)
title: Proprietà Ordinal (ADO MD cell) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 55db23316b4d920154f00aa3b03fb101b2382483
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440813"
---
# <a name="ordinal-property-ado-md-cell"></a>Proprietà Ordinal (Cell - ADO MD)
Identifica in modo univoco una [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md) in base alla relativa posizione all'interno di un oggetto Cell.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore ordinale della cella identifica in modo univoco la cella all'interno di un celle. Dal punto di vista concettuale, le celle sono numerate in un insieme di celle come se il numero di celle fosse una matrice *p*-dimensionale, dove *p* è il numero di [assi](../../../ado/reference/ado-md-api/axes-collection-ado-md.md). Le celle sono numerate a partire da zero nell'ordine principale della riga. Di seguito è illustrata la formula per il calcolo del numero ordinale di una cella:  
  
 Il valore ordinale della cella può essere utilizzato con la proprietà [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) dell'oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) per recuperare rapidamente la [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di asse (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Oggetto cellt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Proprietà Item (ADO MD Cellt)](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)   
 [Proprietà Ordinal (Position - ADO MD)](../../../ado/reference/ado-md-api/ordinal-property-ado-md-position.md)
