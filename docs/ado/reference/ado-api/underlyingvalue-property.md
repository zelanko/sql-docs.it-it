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
ms.openlocfilehash: 582d0b87edd4729ce54cc2a7323b0a63443cab82
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938850"
---
# <a name="underlyingvalue-property"></a>Proprietà UnderlyingValue
Indica il valore corrente di un oggetto [campo](../../../ado/reference/ado-api/field-object.md) nel database.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Variant** che indica il valore del **campo**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **UnderlyingValue** per restituire il valore del campo corrente dal database. Il valore del campo nella proprietà **UnderlyingValue** è il valore visibile alla transazione e può essere il risultato di un aggiornamento recente da parte di un'altra transazione. Questo può differire dalla proprietà [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) , che riflette il valore restituito in origine al [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Questo metodo è simile all'utilizzo del metodo [Resync](../../../ado/reference/ado-api/resync-method.md) , ma la proprietà **UnderlyingValue** restituisce solo il valore per un campo specifico del record corrente. Si tratta dello stesso valore utilizzato dal metodo [Resync](../../../ado/reference/ado-api/resync-method.md) per sostituire la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 Quando si usa questa proprietà con la proprietà **OriginalValue** , è possibile risolvere i conflitti che si verificano da aggiornamenti batch.  
  
## <a name="record"></a>Record  
 Per gli oggetti [record](../../../ado/reference/ado-api/record-object-ado.md) , questa proprietà sarà vuota per i campi aggiunti prima della chiamata a [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà OriginalValue e UnderlyingValue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Esempio di proprietà OriginalValue e UnderlyingValue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Proprietà OriginalValue (ADO)](../../../ado/reference/ado-api/originalvalue-property-ado.md)   
 [Metodo Resync](../../../ado/reference/ado-api/resync-method.md)
