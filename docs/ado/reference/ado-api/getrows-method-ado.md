---
title: Metodo GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d96b7968c7aba8d1249db2f43b53fc8a22596419
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918457"
---
# <a name="getrows-method-ado"></a>Metodo GetRows (ADO)
Recupera più record di un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) in una matrice.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una **variante** il cui valore è una matrice bidimensionale.  
  
#### <a name="parameters"></a>Parametri  
 *righe*  
 Facoltativo. Valore [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) che indica il numero di record da recuperare. Il valore predefinito è **adGetRowsRest**.  
  
 *Inizia*  
 Facoltativo. Valore **stringa** o **variante** che restituisce il segnalibro per il record da cui deve iniziare l'operazione **GetRows** . È anche possibile usare un valore [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) .  
  
 *Fields*  
 Facoltativo. **Variant** che rappresenta un nome di campo singolo o una posizione ordinale o una matrice di nomi di campo o numeri di posizione ordinale. ADO restituisce solo i dati in questi campi.  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **GetRows** per copiare record da un **Recordset** in una matrice bidimensionale. Il primo indice identifica il campo e il secondo identifica il numero di record. La variabile di *matrice* viene dimensionata automaticamente con le dimensioni corrette quando il metodo **GetRows** restituisce i dati.  
  
 Se non si specifica un valore per l'argomento *Rows* , il metodo **GetRows** recupera automaticamente tutti i record nell'oggetto **Recordset** . Se si richiedono più record di quanti siano disponibili, **GetRows** restituisce solo il numero di record disponibili.  
  
 Se l'oggetto **Recordset** supporta segnalibri, è possibile specificare in quale record il metodo **GetRows** deve iniziare a recuperare i dati passando il valore della proprietà [segnalibro](../../../ado/reference/ado-api/bookmark-property-ado.md) di tale record nell'argomento *iniziale* .  
  
 Se si desidera limitare i campi restituiti dalla chiamata **GetRows** , è possibile passare un nome/numero di campo singolo o una matrice di nomi di campo/numeri nell'argomento *Fields* .  
  
 Dopo aver chiamato **GetRows**, il successivo record non letto diventa il record corrente oppure la proprietà [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è impostata su **true** se non sono presenti altri record.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esempio di metodo GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Esempio del metodo GetRows (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
