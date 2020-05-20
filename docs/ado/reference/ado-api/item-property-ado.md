---
title: Proprietà Item (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a5925bc0e2ab4991c1067c6d1c26cfff2c237b37
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763432"
---
# <a name="item-property-ado"></a>Proprietà Item (ADO)
Indica un membro specifico di una raccolta, in base al nome o al numero ordinale.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un riferimento a un oggetto.  
  
## <a name="parameters"></a>Parametri  
 *Indice*  
 Espressione **Variant** che restituisce il nome o il numero ordinale di un oggetto in una raccolta.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Item** per restituire un oggetto specifico in una raccolta. Se **Item** non riesce a trovare un oggetto nella raccolta corrispondente all'argomento *index* , si verificherà un errore. Inoltre, alcune raccolte non supportano gli oggetti denominati; per queste raccolte, è necessario usare i riferimenti numerici ordinali.  
  
 La proprietà **Item** è la proprietà predefinita per tutte le raccolte. Pertanto, i seguenti formati di sintassi sono intercambiabili:  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Raccolta di oggetti Column (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Raccolta Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Raccolta di oggetti Group (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Raccolta di oggetti Index (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Raccolta Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Item (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Esempio della proprietà Item (VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
