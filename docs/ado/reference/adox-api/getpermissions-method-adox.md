---
title: Metodo GetPermissions (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8bff406485266af99a1c2538a4df237fd5bf43bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712086"
---
# <a name="getpermissions-method-adox"></a>Metodo GetPermissions (ADOX)
Restituisce le autorizzazioni per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) oppure [utente](../../../ado/reference/adox-api/user-object-adox.md) su un oggetto o un contenitore di oggetti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore che specifica una maschera di bit che contiene le autorizzazioni che il gruppo o l'utente dispone sull'oggetto. Questo valore può essere uno o più i [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) costanti.  
  
#### <a name="parameters"></a>Parametri  
 *Name*  
 Oggetto **Variant** valore che specifica il nome dell'oggetto per cui impostare le autorizzazioni. Impostare *nome* su un valore null se si desidera ottenere le autorizzazioni per il contenitore di oggetti.  
  
 *ObjectType*  
 Oggetto **lungo** valore che può essere uno del [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) costanti, che specifica il tipo dell'oggetto per cui ottenere le autorizzazioni.  
  
 *ObjectTypeId*  
 Facoltativo. Oggetto **Variant** valore che specifica il GUID per un tipo di oggetto provider non è definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostata su **impostato su adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [GetPermissions e SetPermissions metodi (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Proprietà Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Metodo SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
