---
description: Metodo GetSchemaObject (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b0a54b02cf748d8ff1144e50e3531295dbfe8c55
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778120"
---
# <a name="getschemaobject-method-ado-md"></a>Metodo GetSchemaObject (ADO MD)
Recupera un oggetto ADO MD schema ([dimensione](./dimension-object-ado-md.md), [gerarchia](./hierarchy-object-ado-md.md), [livello](./level-object-ado-md.md)o [membro](./member-object-ado-md.md)) in base al relativo [UniqueName](./uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjType*  
 Valore [SchemaObjectTypeEnum](./schemaobjecttypeenum.md) che specifica il tipo di oggetto dello schema (dimensione, gerarchia, livello o membro) da recuperare.  
  
 *UniqueName*  
 **Stringa** che specifica il valore della proprietà **UniqueName** dell'oggetto da recuperare.  
  
## <a name="remarks"></a>Commenti  
 **GetSchemaObject** recupera gli oggetti usando i rispettivi nomi univoci, come specificato dalla proprietà **UniqueName** . Non è necessario che i nomi degli oggetti padre siano noti e non è necessario popolare le raccolte padre per recuperare un oggetto dello schema.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto CubeDef (ADO MD)](./cubedef-object-ado-md.md)