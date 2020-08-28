---
description: StringFormatEnum
title: StringFormatEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fe580d45d20c65c313cd87b3fb47ef63bb349ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988422"
---
# <a name="stringformatenum"></a>StringFormatEnum
Specifica il formato durante il recupero di un [Recordset](./recordset-object-ado.md) come stringa.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adClipString**|2|Delimita le righe in base a *RowDelimiter*, colonne per *ColumnDelimiter*e valori null per *NullExpr*. Questi tre parametri del metodo [GetString](./getstring-method-ado.md) sono validi solo con un *StringFormat* di **adClipString**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. StringFormat. CLIPSTRING|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo GetString (ADO)](./getstring-method-ado.md)