---
title: Proprietà UnderlyingValue | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d946e744fe3b3e5fba12f83067dc751296b58ac6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710540"
---
# <a name="underlyingvalue-property"></a>Proprietà UnderlyingValue
Indica il valore corrente di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto nel database.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Variant** valore che indica il valore della **campo**.  
  
## <a name="remarks"></a>Note  
 Usare la **UnderlyingValue** proprietà per restituire il valore del campo corrente dal database. Il valore del campo nel **UnderlyingValue** proprietà è il valore che è visibile alla transazione e può essere il risultato di un recente aggiornamento da un'altra transazione. Questo può differire dal [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) proprietà, che riflette il valore che è stato originariamente restituito per il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 È simile all'uso di [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo, ma la **UnderlyingValue** proprietà restituisce solo il valore per un campo specifico del record corrente. Questo è lo stesso valore che il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo utilizzato per sostituire la [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà.  
  
 Quando si usa questa proprietà con il **OriginalValue** proprietà, è possibile risolvere i conflitti generati dagli aggiornamenti batch.  
  
## <a name="record"></a>Record  
 Per la [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetti, questa proprietà sarà vuota per i campi aggiunti prima [Update](../../../ado/reference/ado-api/update-method.md) viene chiamato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di OriginalValue e UnderlyingValue (esempio di proprietà (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Esempio di OriginalValue e UnderlyingValue in proprietà XML (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Proprietà OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Metodo Resync](../../../ado/reference/ado-api/resync-method.md)
