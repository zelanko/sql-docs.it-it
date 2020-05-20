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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a2bbb889bc0277ab01f29896d4f60eebd8236cb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759167"
---
# <a name="getpermissions-method-adox"></a>Metodo GetPermissions (ADOX)
Restituisce le autorizzazioni per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) o un [utente](../../../ado/reference/adox-api/user-object-adox.md) in un contenitore oggetto o oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** che specifica una maschera di maschera contenente le autorizzazioni del gruppo o dell'utente nell'oggetto. Questo valore può essere costituito da una o più costanti [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) .  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 Valore **Variant** che specifica il nome dell'oggetto per il quale impostare le autorizzazioni. Impostare *nome* su un valore null se si desidera ottenere le autorizzazioni per il contenitore di oggetti.  
  
 *ObjectType*  
 Valore **Long** che può essere una delle costanti [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , che specifica il tipo dell'oggetto per il quale ottenere le autorizzazioni.  
  
 *ObjectTypeId*  
 Facoltativa. Valore **Variant** che specifica il GUID per un tipo di oggetto provider non definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostato su **adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetPermissions e sepermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Proprietà Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Metodo SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
