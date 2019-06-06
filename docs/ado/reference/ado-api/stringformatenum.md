---
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StringFormatEnum
helpviewer_keywords:
- StringFormatEnum enumeration [ADO]
ms.assetid: 28f7d1ec-092b-4323-a39d-d3f882c6c81a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7225f8a7612f08947720eb2912722dc92b7a2a96
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710802"
---
# <a name="stringformatenum"></a>StringFormatEnum
Specifica il formato durante il recupero di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sotto forma di stringa.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita le righe da *RowDelimiter*, le colonne da *ColumnDelimiter*e i valori da null *NullExpr*. Questi tre parametri del [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) metodo sono validi solo con un *StringFormat* dei **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.StringFormat.CLIPSTRING|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
