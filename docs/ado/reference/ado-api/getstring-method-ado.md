---
description: Metodo GetString (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ef3d32e1caae337ecb2a03bba6af8c7b4cd858de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443513"
---
# <a name="getstring-method-ado"></a>Metodo GetString (ADO)
Restituisce il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sotto forma di stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il **Recordset** come **Variant** con valori di stringa (BSTR).  
  
#### <a name="parameters"></a>Parametri  
 *StringFormat*  
 Valore [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md) che specifica la modalità di conversione del **Recordset** in una stringa. I parametri *RowDelimiter*, *ColumnDelimiter*e *NullExpr* vengono utilizzati solo con un oggetto *StringFormat* di **adClipString**.  
  
 *NumRows*  
 Facoltativo. Numero di righe da convertire nel **Recordset**. Se *NumRows* non è specificato o è maggiore del numero totale di righe nel **Recordset**, tutte le righe nel **Recordset** vengono convertite.  
  
 *ColumnDelimiter*  
 Facoltativo. Un delimitatore utilizzato tra le colonne, se specificato, in caso contrario il carattere di TABULAzione.  
  
 *RowDelimiter*  
 Facoltativo. Un delimitatore utilizzato tra le righe, se specificato, in caso contrario il carattere di ritorno A capo.  
  
 *NullExpr*  
 Facoltativo. Espressione utilizzata al posto di un valore null, se specificato, in caso contrario una stringa vuota.  
  
## <a name="remarks"></a>Osservazioni  
 I dati di riga, ma senza dati dello schema, vengono salvati nella stringa. Pertanto, non è possibile riaprire un **Recordset** utilizzando questa stringa.  
  
 Questo metodo è equivalente al metodo **GetClipString** di RDO.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
