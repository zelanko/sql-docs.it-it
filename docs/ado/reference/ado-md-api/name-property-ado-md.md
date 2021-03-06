---
description: Proprietà Name (ADO MD)
title: Proprietà Name (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 4dfec86bb631dda661b957e02667cd320c20fec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986242"
---
# <a name="name-property-ado-md"></a>Proprietà Name (ADO MD)
Indica il nome di un oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile recuperare la proprietà **Name** di un oggetto in base a un riferimento ordinale, dopo di che è possibile fare riferimento all'oggetto direttamente in base al nome. Se, ad esempio, `cdf.CubeDefs(0).Name` produce "Bob video store", è possibile fare riferimento a questo [CubeDef](./cubedef-object-ado-md.md) come `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Axis (ADO MD)](./axis-object-ado-md.md)  
        [Oggetto Catalog (ADO MD)](./catalog-object-ado-md.md)  
        [Oggetto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Oggetto Dimension (ADO MD)](./dimension-object-ado-md.md)  
        [Oggetto Hierarchy (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Oggetto Level (ADO MD)](./level-object-ado-md.md)  
        [Oggetto Member (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di catalogo (VB)](./catalog-example-vb.md)   
 [Proprietà Caption (ADO MD)](./caption-property-ado-md.md)   
 [Proprietà Description (ADO MD)](./description-property-ado-md.md)   
 [Proprietà UniqueName (ADO MD)](./uniquename-property-ado-md.md)