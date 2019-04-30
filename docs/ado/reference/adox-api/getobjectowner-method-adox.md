---
title: Metodo GetObjectOwner (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b2c967ac293ed59fde6494e12c2afc2c5b6de90
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63464721"
---
# <a name="getobjectowner-method-adox"></a>Metodo GetObjectOwner (ADOX)
Restituisce il proprietario di un oggetto in un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **stringa** valore che specifica il [nome](../../../ado/reference/adox-api/name-property-adox.md) del [utente](../../../ado/reference/adox-api/user-object-adox.md) oppure [gruppo](../../../ado/reference/adox-api/group-object-adox.md) che possiede l'oggetto.  
  
#### <a name="parameters"></a>Parametri  
 *ObjectName*  
 Oggetto **stringa** valore che specifica il nome dell'oggetto per cui restituire il proprietario.  
  
 *ObjectType*  
 Oggetto **lungo** valore che può essere uno del [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) costanti, che specifica il tipo dell'oggetto per cui ottenere il proprietario.  
  
 *ObjectTypeId*  
 Facoltativo. Oggetto **Variant** valore che specifica il GUID per un tipo di oggetto provider non è definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostata su **impostato su adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Note  
 Se il provider non supporta la restituzione i proprietari degli oggetti, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [GetObjectOwner e SetObjectOwner metodi (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Metodo SetObjectOwner (ADOX)](../../../ado/reference/adox-api/setobjectowner-method.md)
