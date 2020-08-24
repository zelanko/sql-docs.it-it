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
ms.openlocfilehash: a0217267b73a449e40beff1134b3cdcc744246f3
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777930"
---
# <a name="ordinal-property-ado-md-cell"></a>Proprietà Ordinal (Cell - ADO MD)
Identifica in modo univoco una [cella](./cell-object-ado-md.md) in base alla relativa posizione all'interno di un oggetto Cell.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Long** integer ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 Il valore ordinale della cella identifica in modo univoco la cella all'interno di un celle. Dal punto di vista concettuale, le celle sono numerate in un insieme di celle come se il numero di celle fosse una matrice *p*-dimensionale, dove *p* è il numero di [assi](./axes-collection-ado-md.md). Le celle sono numerate a partire da zero nell'ordine principale della riga. Di seguito è illustrata la formula per il calcolo del numero ordinale di una cella:  
  
 Il valore ordinale della cella può essere utilizzato con la proprietà [Item](./item-property-ado-md-cellset.md) dell'oggetto [cellt](./cellset-object-ado-md.md) per recuperare rapidamente la [cella](./cell-object-ado-md.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di asse (VBScript)](./axis-example-vbscript.md)   
 [Oggetto cellt (ADO MD)](./cellset-object-ado-md.md)   
 [Proprietà Item (ADO MD Cellt)](./item-property-ado-md-cellset.md)   
 [Proprietà Ordinal (Position - ADO MD)](./ordinal-property-ado-md-position.md)