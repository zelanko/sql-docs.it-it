---
title: Proprietà Attributes (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: rothja
ms.author: jroth
ms.openlocfilehash: 488fe5a46b994ed664c6355e24fe8d567d5ff11d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762908"
---
# <a name="attributes-property-ado"></a>Proprietà Attributes (ADO)
Indica una o più caratteristiche di un oggetto.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** .  
  
 Per un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) , la proprietà **Attributes** è di lettura/scrittura e il relativo valore può essere la somma di uno o più valori [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) . Il valore predefinito è zero (0).  
  
 Per un oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) , la proprietà **Attributes** è di lettura/scrittura e il relativo valore può essere la somma di uno o più valori [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) . Il valore predefinito è **adParamSigned**.  
  
 Per un oggetto [campo](../../../ado/reference/ado-api/field-object.md) , la proprietà **Attributes** può essere la somma di uno o più valori [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) . In genere è di sola lettura. Tuttavia, per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un [record](../../../ado/reference/ado-api/record-object-ado.md), **gli attributi** sono di lettura/scrittura solo dopo che è stata specificata la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) per il **campo** e il nuovo **campo** è stato aggiunto correttamente dal provider di dati chiamando il metodo [Update](../../../ado/reference/ado-api/update-method.md) della raccolta **Fields** .  
  
 Per un oggetto [Proprietà](../../../ado/reference/ado-api/property-object-ado.md) , la proprietà **Attributes** è di sola lettura e il relativo valore può essere la somma di uno o più valori [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Attributes** per impostare o restituire le caratteristiche di oggetti **connessione** , oggetti **parametro** , oggetti **campo** o oggetti **Property** .  
  
 Quando si impostano più attributi, è possibile sommare le costanti appropriate. Se si imposta il valore della proprietà su una somma, incluse le costanti incompatibili, si verificherà un errore.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Questa proprietà non è disponibile in un oggetto **connessione** sul lato client.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Attributes e Name (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Esempio di proprietà Attributes e Name (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Metodo AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Metodi BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Metodo GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
