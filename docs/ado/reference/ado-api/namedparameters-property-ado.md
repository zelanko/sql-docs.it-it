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
author: rothja
ms.author: jroth
ms.openlocfilehash: 432a4968a301e51c1ca69e3b84ea80e0a19e32bb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762412"
---
# <a name="namedparameters-property-ado"></a>Proprietà NamedParameters (ADO)
Indica se i nomi dei parametri devono essere passati al provider.  
  
## <a name="remarks"></a>Osservazioni  
 Quando questa proprietà è true, ADO passa il valore della proprietà **Name** di ogni parametro nella raccolta di **parametri** per l' [oggetto Command](../../../ado/reference/ado-api/command-object-ado.md). Il provider usa un nome di parametro per trovare la corrispondenza con i parametri nelle proprietà **CommandText** o **CommandStream** . Se questa proprietà è false (impostazione predefinita), i nomi dei parametri vengono ignorati e il provider usa l'ordine dei parametri per confrontare i valori con i parametri nelle proprietà **CommandText** o **CommandStream** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Proprietà CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
