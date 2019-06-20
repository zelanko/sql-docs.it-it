---
title: Proprietà NamedParameters (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce517f4ba3f2fc4a80932024a8fe51ac285cdb7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707300"
---
# <a name="namedparameters-property-ado"></a>Proprietà NamedParameters (ADO)
Indica se i nomi dei parametri deve essere passati al provider.  
  
## <a name="remarks"></a>Note  
 Quando questa proprietà è true, ADO passa il valore del **Name** proprietà di ogni parametro nel **parametro** raccolta per il [oggetto comando](../../../ado/reference/ado-api/command-object-ado.md). Il provider utilizza un nome di parametro per corrispondere ai parametri in di **CommandText** oppure **CommandStream** proprietà. Se questa proprietà è false (impostazione predefinita), i nomi dei parametri vengono ignorati e il provider Usa l'ordine dei parametri in modo che corrispondano ai parametri in valori di **CommandText** oppure **CommandStream** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Proprietà CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Raccolta di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
