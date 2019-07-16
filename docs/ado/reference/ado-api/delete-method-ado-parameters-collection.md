---
title: Metodo Delete (insieme di parametri ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Delete
- _DynaCollection::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 160c575e-df63-4ade-a2d3-5fd8f72e70cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 965ef1bc84961e3358c530180bfe4e99249b0bc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933171"
---
# <a name="delete-method-ado-parameters-collection"></a>Metodo Delete (raccolta Parameters ADO)
Elimina un oggetto dal [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parametri  
 *Index*  
 Oggetto **stringa** valore contenente il nome dell'oggetto che si desidera eliminare, o la posizione ordinale dell'oggetto (indice) nella raccolta.  
  
## <a name="remarks"></a>Note  
 Usando il **eliminare** metodo in una raccolta consente di rimuovere uno degli oggetti nella raccolta. Questo metodo è disponibile solo per i **parametri** raccolta di un [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto. È necessario usare il [parametro](../../../ado/reference/ado-api/parameter-object.md) dell'oggetto [Name](../../../ado/reference/ado-api/name-property-ado.md) proprietà o l'indice di raccolta quando si chiama il **Elimina** variabile (metodo), un oggetto non è un argomento valido.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di parametri (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Elimina metodo (Recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Metodo DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
