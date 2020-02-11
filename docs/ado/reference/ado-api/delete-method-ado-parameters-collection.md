---
title: Metodo Delete (raccolta Parameters ADO) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933171"
---
# <a name="delete-method-ado-parameters-collection"></a>Metodo Delete (raccolta Parameters ADO)
Elimina un oggetto dalla raccolta di [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Parameters.Delete Index  
```  
  
#### <a name="parameters"></a>Parametri  
 *Indice*  
 Valore **stringa** che contiene il nome dell'oggetto che si desidera eliminare o la posizione ordinale (indice) dell'oggetto nella raccolta.  
  
## <a name="remarks"></a>Osservazioni  
 L'utilizzo del metodo **Delete** in una raccolta consente di rimuovere uno degli oggetti nella raccolta. Questo metodo è disponibile solo nella raccolta **Parameters** di un oggetto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Quando si chiama il metodo **Delete** , è necessario utilizzare la proprietà [Name](../../../ado/reference/ado-api/name-property-ado.md) dell'oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) o il relativo indice di raccolta. una variabile oggetto non è un argomento valido.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Delete (raccolta di campi ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Metodo DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
