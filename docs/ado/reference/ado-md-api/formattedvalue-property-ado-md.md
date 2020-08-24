---
description: Proprietà FormattedValue (ADO MD)
title: Proprietà FormattedValue (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: ba8b3469d017b79027670cb4de9f8b3761c8dcc7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778130"
---
# <a name="formattedvalue-property-ado-md"></a>Proprietà FormattedValue (ADO MD)
Indica la visualizzazione formattata di un valore di [cella](./cell-object-ado-md.md) .  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare la proprietà **formattedValue** per ottenere il valore di visualizzazione formattato della proprietà [value](./value-property-ado-md.md) di un oggetto [Cell](./cell-object-ado-md.md) . Se ad esempio il valore di una cella è 1056,87 e questo valore rappresenta un importo in dollari, **formattedValue** sarà $1.056,87.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di celle (VB)](./cellset-example-vb.md)   
 [Proprietà Value (ADO MD)](./value-property-ado-md.md)