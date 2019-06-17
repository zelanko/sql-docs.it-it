---
title: Metodo SetObjectOwner | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: befb99993db3369995934be4f8d5874d4753d288
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718827"
---
# <a name="setobjectowner-method"></a>Metodo SetObjectOwner
Specifica il proprietario di un oggetto in un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjectName*  
 Oggetto **stringa** valore che specifica il nome dell'oggetto per cui si desidera specificare il proprietario.  
  
 *ObjectType*  
 Oggetto **lungo** valore che può essere uno del [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) le costanti che specifica il tipo di proprietario.  
  
 *OwnerName*  
 Oggetto **stringa** valore che specifica il [Name](../../../ado/reference/adox-api/name-property-adox.md) del [utente](../../../ado/reference/adox-api/user-object-adox.md) o [gruppo](../../../ado/reference/adox-api/group-object-adox.md) al proprietario dell'oggetto.  
  
 *ObjectTypeId*  
 Facoltativo. Oggetto **Variant** valore che specifica il GUID per un tipo di oggetto provider che non è definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostata su **impostato su adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Note  
 Se il provider non supporta specificando i proprietari degli oggetti, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [GetObjectOwner e SetObjectOwner metodi (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Metodo GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
