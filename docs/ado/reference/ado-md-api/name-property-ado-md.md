---
title: Proprietà Name (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 40a392e355e2ec8a468034b382956489f554ac78
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243132"
---
# <a name="name-property-ado-md"></a>Proprietà Name (ADO MD)
Indica il nome di un oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Commenti  
 È possibile recuperare la proprietà **Name** di un oggetto in base a un riferimento ordinale, dopo di che è possibile fare riferimento all'oggetto direttamente in base al nome. Se, ad esempio, `cdf.CubeDefs(0).Name` produce "Bob video store", è possibile fare riferimento a questo [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) come `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)  
        [Oggetto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)  
        [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Oggetto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)  
        [Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Oggetto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)  
        [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di catalogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Proprietà Caption (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Proprietà Description (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [Proprietà UniqueName (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
