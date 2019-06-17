---
title: Proprietà OriginalValue (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e9a576220d7771ed539765da2947f6a7cc750f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706922"
---
# <a name="originalvalue-property-ado"></a>Proprietà OriginalValue (ADO)
Indica il valore di una [campo](../../../ado/reference/ado-api/field-object.md) che era presente nel record prima che venissero apportate le modifiche.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Variant** valore che rappresenta il valore di un campo prima di qualsiasi modifica apportata.  
  
## <a name="remarks"></a>Note  
 Usare la **OriginalValue** proprietà per restituire il valore originale del campo per un campo del record corrente.  
  
 In *modalità di aggiornamento immediato* (in cui il provider scrive le modifiche all'origine dati sottostante dopo aver chiamato il [aggiornare](../../../ado/reference/ado-api/update-method.md) metodo), il **OriginalValue** restituisce proprietà il valore del campo esistente prima di eventuali modifiche (vale a dire, dopo l'ultimo **Update** chiamata al metodo). Questo è lo stesso valore che il [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo utilizzato per sostituire le [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà.  
  
 Nella *modalità di aggiornamento batch* (in cui il provider vengono memorizzati nella cache più modifiche e li scrive all'origine dati sottostante solo quando si chiama il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo), il **OriginalValue** proprietà restituisce il valore del campo esistente prima di eventuali modifiche (vale a dire, dopo l'ultimo **UpdateBatch** chiamata al metodo). Questo è lo stesso valore che il [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodo utilizzato per sostituire le **valore** proprietà. Quando si usa questa proprietà con il [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) proprietà, è possibile risolvere i conflitti generati dagli aggiornamenti batch.  
  
## <a name="record"></a>Record  
 Per la [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetti, il **OriginalValue** proprietà sarà vuota per i campi aggiunti prima [Update](../../../ado/reference/ado-api/update-method.md) viene chiamato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di OriginalValue e UnderlyingValue (esempio di proprietà (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Esempio di OriginalValue e UnderlyingValue in proprietà XML (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Proprietà UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
