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
ms.openlocfilehash: 512569ce2baa8acabdf8bcbf8f637ebf20e4f613
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917838"
---
# <a name="originalvalue-property-ado"></a>Proprietà OriginalValue (ADO)
Indica il valore di un [campo](../../../ado/reference/ado-api/field-object.md) esistente nel record prima che siano state apportate modifiche.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Variant** che rappresenta il valore di un campo prima di qualsiasi modifica.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **OriginalValue** per restituire il valore del campo originale per un campo dal record corrente.  
  
 In *modalità di aggiornamento immediato* (in cui il provider scrive le modifiche nell'origine dati sottostante dopo aver chiamato il metodo [Update](../../../ado/reference/ado-api/update-method.md) ), la proprietà **OriginalValue** restituisce il valore del campo esistente prima delle modifiche, ovvero dall'ultima chiamata al metodo **Update** . Si tratta dello stesso valore utilizzato dal metodo [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) per sostituire la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) .  
  
 In *modalità di aggiornamento batch* (in cui il provider memorizza nella cache più modifiche e le scrive nell'origine dati sottostante solo quando si chiama il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) ), la proprietà **OriginalValue** restituisce il valore del campo esistente prima delle modifiche (ovvero, dall'ultima chiamata al metodo **UpdateBatch** ). Si tratta dello stesso valore utilizzato dal metodo [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) per sostituire la proprietà **value** . Quando si usa questa proprietà con la proprietà [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) , è possibile risolvere i conflitti che si verificano da aggiornamenti batch.  
  
## <a name="record"></a>Record  
 Per gli oggetti [record](../../../ado/reference/ado-api/record-object-ado.md) , la proprietà **OriginalValue** sarà vuota per i campi aggiunti prima della chiamata a [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà OriginalValue e UnderlyingValue (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [Esempio di proprietà OriginalValue e UnderlyingValue (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [Proprietà UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
