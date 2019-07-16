---
title: Metodo Delete (raccolta Fields ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields20::Delete
- Fields20::raw_Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 25bedc25-c51c-4cab-96ce-930b959965d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9db49905b6548e5cb21cca976683c8b387017d32
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919130"
---
# <a name="delete-method-ado-fields-collection"></a>Metodo Delete (raccolta Fields ADO)
Elimina un oggetto dal [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Fields.Delete Field  
```  
  
#### <a name="parameters"></a>Parametri  
 *Campo*  
 Oggetto **Variant** che definisce il [campo](../../../ado/reference/ado-api/field-object.md) oggetto da eliminare. Questo parametro può essere il nome del **campo** oggetto o la posizione ordinale della **campo** oggetto stesso.  
  
## <a name="remarks"></a>Note  
 Chiama il **Fields. Delete** metodo su un elemento aperto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) provoca un errore di run-time.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Delete (insieme di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Elimina metodo (Recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Metodo DeleteRecord (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
