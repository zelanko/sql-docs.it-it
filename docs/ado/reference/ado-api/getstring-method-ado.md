---
title: Metodo GetString (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1570918c423291b6c4fdd212fcb82f518dfb766e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028198"
---
# <a name="getstring-method-ado"></a>Metodo GetString (ADO)
Restituisce il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sotto forma di stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il **Recordset** come una stringa con valori di **Variant** (BSTR).  
  
#### <a name="parameters"></a>Parametri  
 *StringFormat*  
 Oggetto [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md) valore che specifica come il **Recordset** devono essere convertite in una stringa. Il *RowDelimiter*, *ColumnDelimiter*, e *NullExpr* parametri vengono utilizzati solo con un *StringFormat* di  **adClipString**.  
  
 *NumRows*  
 Facoltativo. Il numero di righe da convertire nel **Recordset**. Se *NumRows* non viene specificato, oppure se è maggiore del numero totale di righe nel **Recordset**, quindi tutte le righe nel **Recordset** vengono convertiti.  
  
 *ColumnDelimiter*  
 Facoltativo. Delimitatore utilizzato tra le colonne, se specificato, in caso contrario, il carattere di tabulazione.  
  
 *RowDelimiter*  
 Facoltativo. Delimitatore utilizzato tra le righe, se specificato, in caso contrario, il carattere di ritorno a capo.  
  
 *NullExpr*  
 Facoltativo. Espressione utilizzata al posto di un valore null, se specificato, in caso contrario una stringa vuota.  
  
## <a name="remarks"></a>Note  
 Dati delle righe, ma non i dati dello schema, viene salvato nella stringa. Pertanto, un **Recordset** non può essere riaperto utilizzando questa stringa.  
  
 Questo metodo equivale al RDO **GetClipString** (metodo).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
