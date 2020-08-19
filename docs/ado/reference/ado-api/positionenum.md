---
description: PositionEnum
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
ms.openlocfilehash: 326fc4f1b9b77c8a4470fedc7d55f2d379aff6f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442713"
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

:::row:::
    :::column:::
        [Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::
