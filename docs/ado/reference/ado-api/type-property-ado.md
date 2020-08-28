---
description: Proprietà Type (ADO)
title: Proprietà Type (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f4dcfd3c22363ab4950e03844647f990a34f4d5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988312"
---
# <a name="type-property-ado"></a>Proprietà Type (ADO)
Indica il tipo operativo o il tipo di dati di un [parametro](./parameter-object.md), un [campo](./field-object.md)o un oggetto [proprietà](./property-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [DataTypeEnum](./datatypeenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Per gli oggetti **Parameter** , la proprietà **Type** è di lettura/scrittura. Per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](./fields-collection-ado.md) di un [record](./record-object-ado.md), il **tipo** è in lettura/scrittura solo dopo che è stata specificata la proprietà [value](./value-property-ado.md) per il **campo** e il provider di dati ha aggiunto correttamente il nuovo **campo** chiamando il metodo [Update](./update-method.md) della raccolta **Fields** .  
  
 Per tutti gli altri oggetti, la proprietà **Type** è di sola lettura.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Field](./field-object.md)  
    :::column-end:::
    :::column:::
        [Oggetto Parameter](./parameter-object.md)  
    :::column-end:::
    :::column:::
        [Oggetto Property (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Type (Field) (VB)](./type-property-example-field-vb.md)   
 [Esempio di proprietà Type (Property) (VC + +)](./type-property-example-property-vc.md)   
 [Proprietà RecordType (ADO)](./recordtype-property-ado.md)   
 [Proprietà Type (Stream - ADO)](./type-property-ado-stream.md)