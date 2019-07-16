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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932101"
---
# <a name="numericscale-property-ado"></a>Proprietà NumericScale (ADO)
Indica la scala di valori numerici in una [parametri](../../../ado/reference/ado-api/parameter-object.md) oppure [campo](../../../ado/reference/ado-api/field-object.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **Byte** valore che indica il numero di posizioni decimali in cui i valori numerici verranno risolte.  
  
## <a name="remarks"></a>Note  
 Usare la **NumericScale** proprietà per determinare il numero di cifre a destra del separatore decimale che sarà utilizzato per rappresentare i valori per un valore numerico **parametro** oppure **campo** oggetto.  
  
 Per la **parametri** oggetti, il **NumericScale** è di lettura/scrittura.  
  
 Per un **campo**oggetto **NumericScale** viene in genere di sola lettura. Tuttavia, per i nuovi **campo** gli oggetti che sono stati accodati per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** è lettura/scrittura solo dopo che il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà per il **campo** è stato specificato e il provider di dati è stato aggiunto il nuovo **campo** chiamando il [ Update](../../../ado/reference/ado-api/update-method.md) metodo per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio NumericScale e Precision Properties (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [Esempio NumericScale e Precision Properties (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Proprietà Precision (ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
