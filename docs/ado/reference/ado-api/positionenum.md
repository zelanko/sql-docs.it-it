---
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 57a440a97dcdf1c0fddcff8017e0c2d04967b92d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763342"
---
# <a name="positionenum"></a>PositionEnum
Specifica la posizione corrente del puntatore del record all'interno di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica che il puntatore al record corrente si trova in BOF (ovvero la proprietà [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**).|  
|**adPosEOF**|-3|Indica che il puntatore al record corrente si trova in EOF (ovvero la proprietà [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**).|  
|**adPosUnknown**|-1|Indica che il **Recordset** è vuoto, che la posizione corrente è sconosciuta oppure il provider non supporta la proprietà [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) o [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) .|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. Position. BOF|  
|AdoEnums. Position. EOF|  
|AdoEnums. Position. UNKNOWN|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
