---
title: Metodo GetSchemaObject (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe681a0f93dd88ad7f4752daf213817c21b054ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043763"
---
# <a name="getschemaobject-method-ado-md"></a>Metodo GetSchemaObject (ADO MD)
Recupera un oggetto dello schema ADO MD ([dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md), oppure [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) dal relativo [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjType*  
 Oggetto [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) valore che specifica il tipo di oggetto dello schema (dimensione, gerarchia, livello o membro) da recuperare.  
  
 *UniqueName*  
 Oggetto **stringa** specificando la **UniqueName** valore della proprietà dell'oggetto da recuperare.  
  
## <a name="remarks"></a>Note  
 **GetSchemaObject** recupera gli oggetti utilizzando i relativi nomi univoci, come specificato dalle **UniqueName** proprietà. I nomi degli oggetti padre non debbano essere noti e le raccolte padre non sono necessario essere popolati per recuperare un oggetto dello schema.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
