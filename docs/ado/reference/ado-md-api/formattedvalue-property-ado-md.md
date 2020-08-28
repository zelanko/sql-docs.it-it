---
description: Proprietà FormattedValue (ADO MD)
title: Proprietà FormattedValue (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 5905b4aba040505c60fa78721718b3ab03c51622
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986702"
---
# <a name="formattedvalue-property-ado-md"></a>Proprietà FormattedValue (ADO MD)
Indica la visualizzazione formattata di un valore di [cella](./cell-object-ado-md.md) .  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **formattedValue** per ottenere il valore di visualizzazione formattato della proprietà [value](./value-property-ado-md.md) di un oggetto [Cell](./cell-object-ado-md.md) . Se ad esempio il valore di una cella è 1056,87 e questo valore rappresenta un importo in dollari, **formattedValue** sarà $1.056,87.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di celle (VB)](./cellset-example-vb.md)   
 [Proprietà Value (ADO MD)](./value-property-ado-md.md)