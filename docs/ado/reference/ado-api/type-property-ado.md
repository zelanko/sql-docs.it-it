---
title: Tipo di proprietà (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02c5b9193b89c131095ccfec6ef185d5ff39f4d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910850"
---
# <a name="type-property-ado"></a>Proprietà Type (ADO)
Indica il tipo di dati o di tipo operativo di una [parametri](../../../ado/reference/ado-api/parameter-object.md), [campo](../../../ado/reference/ado-api/field-object.md), o [proprietà](../../../ado/reference/ado-api/property-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valore.  
  
## <a name="remarks"></a>Note  
 Per la **parametri** oggetti, il **tipo** è di lettura/scrittura. Per ottenere nuove **campo** gli oggetti che sono stati accodati per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md), **tipo** è lettura/scrittura solo dopo il [ Valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà per il **campo** è stato specificato e il provider di dati è stato aggiunto il nuovo **campo** chiamando il [aggiornare](../../../ado/reference/ado-api/update-method.md)metodo per la **campi** raccolta.  
  
 Per tutti gli altri oggetti, il **tipo** proprietà è di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Type (campo) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [Esempio di proprietà Type (proprietà) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [Proprietà RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Proprietà Type (flusso ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
