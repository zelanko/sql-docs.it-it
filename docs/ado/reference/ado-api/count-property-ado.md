---
title: La proprietà Count (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 988ee3dc6cb4b394ee1da170cb902b88fcb0f1ca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308945"
---
# <a name="count-property-ado"></a>Proprietà Count (ADO)
Indica il numero di oggetti in una raccolta.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore.  
  
## <a name="remarks"></a>Note  
 Usare la **conteggio** proprietà per determinare il numero di oggetti inclusi in una raccolta specificata.  
  
 Poiché per i membri di una raccolta di numerazione inizia da zero, è consigliabile codificare sempre i cicli a partire dal membro zero e terminando con il valore della **conteggio** proprietà meno 1. Se si utilizza Microsoft Visual Basic e si desidera eseguire un ciclo attraverso i membri di una raccolta senza il controllo il **conteggio** proprietà, utilizzare il **For Each... Avanti** comando.  
  
 Se il **conteggio** proprietà è zero, non sono presenti oggetti nella raccolta.  
  
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
 [Esempio di proprietà Count (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Esempio di proprietà Count (VC + +)](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Metodo Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
