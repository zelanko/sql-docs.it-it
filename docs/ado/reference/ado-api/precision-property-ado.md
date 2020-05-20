---
title: Proprietà Precision (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: f3a72234a6d5e5cbb8e0dc9f5d625b93f15f437f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763332"
---
# <a name="precision-property-ado"></a>Proprietà Precision (ADO)
Indica il grado di precisione per i valori numerici in un oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) o per gli oggetti [campo](../../../ado/reference/ado-api/field-object.md) numerico.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **byte** che indica il numero massimo di cifre utilizzate per rappresentare i valori.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Precision** per determinare il numero massimo di cifre utilizzate per rappresentare i valori per un **parametro** numerico o un oggetto **campo** .  
  
 Il valore è di lettura/scrittura su un oggetto **Parameter** .  
  
 Per un oggetto **campo**, la **precisione** è in genere di sola lettura. Tuttavia, per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un [record](../../../ado/reference/ado-api/record-object-ado.md), la **precisione** è di lettura/scrittura solo dopo che è stata specificata la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) per il **campo** e il provider di dati ha aggiunto correttamente il nuovo **campo** chiamando il metodo [Update](../../../ado/reference/ado-api/update-method.md) della raccolta **Fields** .  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà NumericScale e Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Esempio di proprietà NumericScale e Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Proprietà NumericScale (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
