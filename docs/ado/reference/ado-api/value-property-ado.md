---
title: Proprietà Value (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e35dd93e6d90a81934d8f272ea79c5eb7c8a97c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67913926"
---
# <a name="value-property-ado"></a>Proprietà Value (ADO)

Indica il valore assegnato a un [campo](../../../ado/reference/ado-api/field-object.md), un [parametro](../../../ado/reference/ado-api/parameter-object.md)o un oggetto [proprietà](../../../ado/reference/ado-api/property-object-ado.md) .
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti

Imposta o restituisce un valore **Variant** che indica il valore dell'oggetto. Il valore predefinito dipende dalla proprietà [Type](../../../ado/reference/ado-api/type-property-ado.md) .
  
## <a name="remarks"></a>Osservazioni

Utilizzare la proprietà **value** per impostare o restituire dati da oggetti **campo** , per impostare o restituire valori di parametro con oggetti **Parameter** oppure per impostare o restituire le impostazioni delle proprietà con oggetti **Property** . Il fatto che la proprietà **value** sia di lettura/scrittura o di sola lettura dipenda da numerosi fattori. Per ulteriori informazioni, vedere gli argomenti relativi agli oggetti.

ADO consente di impostare e restituire dati binari lunghi con la proprietà **value** .
  
> [!NOTE]
> Per gli oggetti **Parameter** , ADO legge la proprietà **value** solo una volta dal provider. Se un comando contiene un **parametro** la cui proprietà **value** è vuota e si crea un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dal comando, assicurarsi di chiudere prima il **Recordset** prima di recuperare la proprietà **value** . In caso contrario, per alcuni provider, la proprietà **value** può essere vuota e non conterrà il valore corretto.
> 
> Per i nuovi oggetti **campo** aggiunti alla raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) , è necessario impostare la proprietà **value** prima di poter specificare altre proprietà del **campo** . Per prima cosa, è necessario assegnare un valore specifico per la proprietà **value** e [aggiornarlo](../../../ado/reference/ado-api/update-method.md) nella raccolta **Fields** denominata. È quindi possibile accedere ad altre proprietà, ad esempio il [tipo](../../../ado/reference/ado-api/type-property-ado.md) o [gli attributi](../../../ado/reference/ado-api/attributes-property-ado.md) .
  
## <a name="applies-to"></a>Si applica a
  
||||  
|-|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Vedere anche

[Esempio di proprietà Value (VB) value,](../../../ado/reference/ado-api/value-property-example-vb.md)
[esempio (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
