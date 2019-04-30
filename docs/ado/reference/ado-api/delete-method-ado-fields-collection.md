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
manager: craigg
ms.openlocfilehash: 097286f14de4dead4490c322615a6405c157f118
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140256"
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
