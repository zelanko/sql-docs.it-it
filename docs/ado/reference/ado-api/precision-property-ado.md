---
description: Proprietà Precision (ADO)
title: Proprietà Precision (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: rothja
ms.author: jroth
ms.openlocfilehash: e7a166077bd0237ff822193297d57dc364d17bef
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990052"
---
# <a name="precision-property-ado"></a>Proprietà Precision (ADO)
Indica il grado di precisione per i valori numerici in un oggetto [Parameter](./parameter-object.md) o per gli oggetti [campo](./field-object.md) numerico.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **byte** che indica il numero massimo di cifre utilizzate per rappresentare i valori.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Precision** per determinare il numero massimo di cifre utilizzate per rappresentare i valori per un **parametro** numerico o un oggetto **campo** .  
  
 Il valore è di lettura/scrittura su un oggetto **Parameter** .  
  
 Per un oggetto **campo**, la **precisione** è in genere di sola lettura. Tuttavia, per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](./fields-collection-ado.md) di un [record](./record-object-ado.md), la **precisione** è di lettura/scrittura solo dopo che è stata specificata la proprietà [value](./value-property-ado.md) per il **campo** e il provider di dati ha aggiunto correttamente il nuovo **campo** chiamando il metodo [Update](./update-method.md) della raccolta **Fields** .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Field](./field-object.md)  
    :::column-end:::
    :::column:::
        [Oggetto Parameter](./parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà NumericScale e Precision (VB)](./numericscale-and-precision-properties-example-vb.md)   
 [Esempio di proprietà NumericScale e Precision (VC + +)](./numericscale-and-precision-properties-example-vc.md)   
 [Proprietà NumericScale (ADO)](./numericscale-property-ado.md)