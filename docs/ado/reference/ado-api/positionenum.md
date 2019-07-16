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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d5f7ca47177a953313ff983bb25f9178b73b4930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917598"
---
# <a name="positionenum"></a>PositionEnum
Specifica la posizione corrente del puntatore del record all'interno di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|Indica che il puntatore di record corrente si trova proprietà BOF (vale a dire il [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è di proprietà **True**).|  
|**adPosEOF**|-3|Indica che il puntatore di record corrente è alla fine del file (vale a dire il [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è di proprietà **True**).|  
|**adPosUnknown**|-1|Indica che il **Recordset** è vuoto, la posizione corrente è sconosciuta, o il provider non supporta la [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) oppure [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) proprietà.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
