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
ms.openlocfilehash: 85bef64902f014e7b5269d6df328128bc8fe8d6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67937887"
---
# <a name="stringformatenum"></a>StringFormatEnum
Specifica il formato durante il recupero di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) come stringa.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita le righe in base a *RowDelimiter*, colonne per *ColumnDelimiter*e valori null per *NullExpr*. Questi tre parametri del metodo [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) sono validi solo con un *StringFormat* di **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. StringFormat. CLIPSTRING|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo GetString (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)
