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
ms.openlocfilehash: 72526eca57d08152d7eaa773be50d68d4b3688e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932466"
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
 Facoltativa. Numero di righe da convertire nel **Recordset**. Se *NumRows* non è specificato o è maggiore del numero totale di righe nel **Recordset**, tutte le righe nel **Recordset** vengono convertite.  
  
 *ColumnDelimiter*  
 Facoltativa. Un delimitatore utilizzato tra le colonne, se specificato, in caso contrario il carattere di TABULAzione.  
  
 *RowDelimiter*  
 Facoltativa. Un delimitatore utilizzato tra le righe, se specificato, in caso contrario il carattere di ritorno A capo.  
  
 *NullExpr*  
 Facoltativa. Espressione utilizzata al posto di un valore null, se specificato, in caso contrario una stringa vuota.  
  
## <a name="remarks"></a>Osservazioni  
 I dati di riga, ma senza dati dello schema, vengono salvati nella stringa. Pertanto, non è possibile riaprire un **Recordset** utilizzando questa stringa.  
  
 Questo metodo è equivalente al metodo **GetClipString** di RDO.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
