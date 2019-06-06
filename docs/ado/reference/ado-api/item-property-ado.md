---
title: Elemento proprietà (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords:
- Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6be26e9c174c1911a0c2c7210552c8e8a0e44a2c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697564"
---
# <a name="item-property-ado"></a>Proprietà Item (ADO)
Indica un membro specifico di una raccolta, per nome o numero ordinale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un riferimento all'oggetto.  
  
## <a name="parameters"></a>Parametri  
 *Index*  
 Oggetto **Variant** espressione che restituisce il nome o al numero ordinale di un oggetto in una raccolta.  
  
## <a name="remarks"></a>Note  
 Usare la **elemento** proprietà per restituire un oggetto specifico in una raccolta. Se **elemento** non è possibile trovare un oggetto nella raccolta corrispondente per il *indice* si verifica un errore di argomento. Inoltre, alcune raccolte non supportano gli oggetti denominati. Per queste raccolte, è necessario usare riferimenti di un numero ordinale.  
  
 Il **elemento** proprietà la proprietà predefinita per tutte le raccolte; pertanto, sono intercambiabili le forme di sintassi seguente:  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Raccolta di oggetti Column (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Raccolta Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Raccolta di errori (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Raccolta di oggetti Group (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Raccolta di oggetti Index (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Raccolta di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Raccolta Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Item (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Esempio di proprietà Item (VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
