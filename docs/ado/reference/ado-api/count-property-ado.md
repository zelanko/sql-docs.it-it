---
title: Proprietà Count (ADO) | Microsoft Docs
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
ms.openlocfilehash: 292a4a8c26b3b10aa47fcbe7046a5897f601ed9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919351"
---
# <a name="count-property-ado"></a>Proprietà Count (ADO)
Indica il numero di oggetti in una raccolta.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **count** per determinare il numero di oggetti in una raccolta specificata.  
  
 Poiché la numerazione per i membri di una raccolta inizia con zero, è consigliabile usare sempre i cicli di codice che iniziano con il membro zero e terminano con il valore della proprietà **count** meno 1. Se si utilizza Microsoft Visual Basic e si desidera scorrere i membri di una raccolta senza selezionare la proprietà **count** , utilizzare l'oggetto **for each... Comando successivo** .  
  
 Se la proprietà **count** è zero, nella raccolta non sono presenti oggetti.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Raccolta Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Raccolta di Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Raccolta Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Raccolta Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Raccolta Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Raccolta Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Raccolta Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Raccolta Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Count (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Esempio di proprietà Count (VC + +)](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Metodo Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
