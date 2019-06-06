---
title: Valore di proprietà (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 68bde5e78c746579bcb34166469569fb594c129f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710273"
---
# <a name="value-property-ado"></a>Proprietà Value (ADO)

Indica il valore assegnato a un [campo](../../../ado/reference/ado-api/field-object.md), [parametro](../../../ado/reference/ado-api/parameter-object.md), o [proprietà](../../../ado/reference/ado-api/property-object-ado.md) oggetto.
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti

Imposta o restituisce un **Variant** valore che indica il valore dell'oggetto. Dipende dal valore predefinito di [tipo](../../../ado/reference/ado-api/type-property-ado.md) proprietà.
  
## <a name="remarks"></a>Note

Usare la **valore** proprietà per impostare o restituire i dati dal **campo** oggetti, per impostare o restituire i valori dei parametri con **parametro** oggetti, o per impostare o restituire le impostazioni delle proprietà con **Proprietà** oggetti. Se il **valore** è di lettura/scrittura o sola lettura dipende da numerosi fattori. Vedere gli argomenti di oggetto corrispondente per altre informazioni.

ADO consente l'impostazione e restituzione di dati binari long con il **valore** proprietà.
  
> [!NOTE]
> Per **parametri** oggetti, le letture ADO le **valore** proprietà una sola volta dal provider. Se un comando contiene un **parametro** cui **valore** proprietà è vuota e si crea un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dal comando, assicurarsi di chiudere il  **Recordset** prima di recuperare il **valore** proprietà. In caso contrario, per alcuni provider, il **valore** proprietà può essere vuota e non deve contenere il valore corretto.
> 
> Per ottenere nuove **campo** gli oggetti che sono stati accodati per il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto, il **valore** deve essere impostata prima di qualsiasi altro **campo** proprietà possono essere specificate. Per prima cosa, un valore specifico per il **valore** proprietà necessario aver assegnata e [Update](../../../ado/reference/ado-api/update-method.md) sul **campi** raccolta denominata. Quindi, le altre proprietà, ad esempio [tipo](../../../ado/reference/ado-api/type-property-ado.md) oppure [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) sono accessibili.
  
## <a name="applies-to"></a>Si applica a
  
||||  
|-|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|
  
## <a name="see-also"></a>Vedere anche

[Valore di esempio di proprietà (Visual Basic)](../../../ado/reference/ado-api/value-property-example-vb.md)
[valore di esempio di proprietà (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
