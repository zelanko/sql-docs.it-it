---
title: Proprietà NumericScale (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38d283e8fedb90ed5a99143090bc6a077efa8512
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932101"
---
# <a name="numericscale-property-ado"></a>Proprietà NumericScale (ADO)
Indica la scala dei valori numerici in un [parametro](../../../ado/reference/ado-api/parameter-object.md) o in un oggetto [campo](../../../ado/reference/ado-api/field-object.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **byte** che indica il numero di posizioni decimali in cui verranno risolti i valori numerici.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **NumericScale** per determinare il numero di cifre a destra del separatore decimale che verranno utilizzate per rappresentare i valori per un **parametro** numerico o un oggetto **campo** .  
  
 Per gli oggetti **Parameter** , la proprietà **NumericScale** è di lettura/scrittura.  
  
 Per un oggetto **Field**, **NumericScale** è in genere di sola lettura. Tuttavia, per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un [record](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** è di lettura/scrittura solo dopo che è stata specificata la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) per il **campo** e il provider di dati ha aggiunto correttamente il nuovo **campo** chiamando il metodo [Update](../../../ado/reference/ado-api/update-method.md) della raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) .  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà NumericScale e Precision (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Esempio di proprietà NumericScale e Precision (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Proprietà Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
