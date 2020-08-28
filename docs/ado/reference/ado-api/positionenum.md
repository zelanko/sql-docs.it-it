---
description: PositionEnum
title: PositionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a871f6d2f7b73e7430761318a5acee31f05df3c1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990072"
---
# <a name="positionenum"></a>PositionEnum
Specifica la posizione corrente del puntatore del record all'interno di un [Recordset](./recordset-object-ado.md).  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica che il puntatore al record corrente si trova in BOF (ovvero la proprietà [BOF](./bof-eof-properties-ado.md) è **true**).|  
|**adPosEOF**|-3|Indica che il puntatore al record corrente si trova in EOF (ovvero la proprietà [EOF](./bof-eof-properties-ado.md) è **true**).|  
|**adPosUnknown**|-1|Indica che il **Recordset** è vuoto, che la posizione corrente è sconosciuta oppure il provider non supporta la proprietà [AbsolutePage](./absolutepage-property-ado.md) o [AbsolutePosition](./absoluteposition-property-ado.md) .|  
  
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
        [Proprietà AbsolutePage (ADO)](./absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [Proprietà AbsolutePosition (ADO)](./absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::