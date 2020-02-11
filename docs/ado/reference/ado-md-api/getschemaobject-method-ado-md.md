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
ms.openlocfilehash: 690c81a46c62c8844780e82b5c82a0ff7301105d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949769"
---
# <a name="getschemaobject-method-ado-md"></a>Metodo GetSchemaObject (ADO MD)
Recupera un oggetto ADO MD schema ([dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md)o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) in base al relativo [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjType*  
 Valore [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) che specifica il tipo di oggetto dello schema (dimensione, gerarchia, livello o membro) da recuperare.  
  
 *UniqueName*  
 **Stringa** che specifica il valore della proprietà **UniqueName** dell'oggetto da recuperare.  
  
## <a name="remarks"></a>Osservazioni  
 **GetSchemaObject** recupera gli oggetti usando i rispettivi nomi univoci, come specificato dalla proprietà **UniqueName** . Non è necessario che i nomi degli oggetti padre siano noti e non è necessario popolare le raccolte padre per recuperare un oggetto dello schema.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
