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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c248139abfd136d5c79658592e0e49d5e10444aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949390"
---
# <a name="name-property-ado-md"></a>Proprietà Name (ADO MD)
Indica il nome di un oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce una **stringa** ed è di sola lettura.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile recuperare la proprietà **Name** di un oggetto in base a un riferimento ordinale, dopo di che è possibile fare riferimento all'oggetto direttamente in base al nome. Se `cdf.CubeDefs(0).Name` , ad esempio, produce "Bob video store", è possibile fare riferimento a questo [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) come `cdf.CubeDefs("Bobs Video Store")`.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Oggetto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Oggetto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Oggetto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Oggetto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di catalogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Proprietà Caption (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Proprietà Description (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [Proprietà UniqueName (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
