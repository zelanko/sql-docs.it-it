---
title: Attributi proprietà (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 91425029546402edbd5bde7df45586c77e38d83b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696391"
---
# <a name="attributes-property-ado"></a>Proprietà Attributes (ADO)
Indica una o più caratteristiche di un oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore.  
  
 Per un [Connection](../../../ado/reference/ado-api/connection-object-ado.md) oggetto, il **attributi** è di lettura/scrittura e il relativo valore può essere la somma di uno o più [XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md) valori. Il valore predefinito è zero (0).  
  
 Per un [parametri](../../../ado/reference/ado-api/parameter-object.md) oggetto, il **attributi** è di lettura/scrittura e il relativo valore può essere la somma di uno o più [ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md) valori. Il valore predefinito è **adParamSigned**.  
  
 Per un [campo](../../../ado/reference/ado-api/field-object.md) oggetti, il **attributi** proprietà può essere la somma di uno o più [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) valori. È in genere di sola lettura. Tuttavia, per il nuovo **campo** gli oggetti che sono stati accodati per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md), **attributi** è solo di lettura/scrittura Dopo che il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà per il **campo** è stato specificato e il nuovo **campo** è stata aggiunta correttamente dal provider di dati chiamando il [ Update](../../../ado/reference/ado-api/update-method.md) metodo per il **campi** raccolta.  
  
 Per un [proprietà](../../../ado/reference/ado-api/property-object-ado.md) oggetti, il **attributi** proprietà è di sola lettura e il relativo valore può essere la somma di uno o più [PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md) valori.  
  
## <a name="remarks"></a>Note  
 Usare il **attributi** proprietà per impostare o restituire le caratteristiche dei **connessione** oggetti, **parametro** oggetti, **campo** oggetti, o **Proprietà** oggetti.  
  
 Quando si impostano più attributi, è possibile sommare le costanti appropriate. Se si imposta il valore della proprietà su una somma, incluse le costanti non compatibile, si verifica un errore.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** questa proprietà non è disponibile in un client-side **connessione** oggetto.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|  
|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Name (VB) e attributi](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Esempio di proprietà Name (VC + +) e attributi](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
 [Metodo AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans e RollbackTrans (ADO)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [Metodo GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
