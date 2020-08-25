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
ms.openlocfilehash: 8a972edd11c419c1990c78635d42c44d8c06db2c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774910"
---
# <a name="getstring-method-ado"></a>Metodo GetString (ADO)
Restituisce il [Recordset](./recordset-object-ado.md) sotto forma di stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce il **Recordset** come **Variant** con valori di stringa (BSTR).  
  
#### <a name="parameters"></a>Parametri  
 *StringFormat*  
 Valore [StringFormatEnum](./stringformatenum.md) che specifica la modalità di conversione del **Recordset** in una stringa. I parametri *RowDelimiter*, *ColumnDelimiter*e *NullExpr* vengono utilizzati solo con un oggetto *StringFormat* di **adClipString**.  
  
 *NumRows*  
 Facoltativa. Numero di righe da convertire nel **Recordset**. Se *NumRows* non è specificato o è maggiore del numero totale di righe nel **Recordset**, tutte le righe nel **Recordset** vengono convertite.  
  
 *ColumnDelimiter*  
 Facoltativa. Un delimitatore utilizzato tra le colonne, se specificato, in caso contrario il carattere di TABULAzione.  
  
 *RowDelimiter*  
 Facoltativa. Un delimitatore utilizzato tra le righe, se specificato, in caso contrario il carattere di ritorno A capo.  
  
 *NullExpr*  
 Facoltativa. Espressione utilizzata al posto di un valore null, se specificato, in caso contrario una stringa vuota.  
  
## <a name="remarks"></a>Commenti  
 I dati di riga, ma senza dati dello schema, vengono salvati nella stringa. Pertanto, non è possibile riaprire un **Recordset** utilizzando questa stringa.  
  
 Questo metodo è equivalente al metodo **GetClipString** di RDO.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio del metodo GetString (VB)](./getstring-method-example-vb.md)