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
ms.openlocfilehash: 50a02898c1694fa43b8bf522a1a1bca65300efda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965232"
---
# <a name="setobjectowner-method"></a>Metodo SetObjectOwner
Specifica il proprietario di un oggetto in un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjectName*  
 Valore **stringa** che specifica il nome dell'oggetto per il quale specificare il proprietario.  
  
 *ObjectType*  
 Valore **Long** che può essere una delle costanti [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) che specifica il tipo di proprietario.  
  
 *OwnerName*  
 Valore **stringa** che specifica il [nome](../../../ado/reference/adox-api/name-property-adox.md) dell' [utente](../../../ado/reference/adox-api/user-object-adox.md) o del [gruppo](../../../ado/reference/adox-api/group-object-adox.md) per il proprietario dell'oggetto.  
  
 *ObjectTypeId*  
 Facoltativa. Valore **Variant** che specifica il GUID per un tipo di oggetto provider non definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostato su **adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Osservazioni  
 Si verificherà un errore se il provider non supporta la specifica di proprietari di oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetObjectOwner e SetObjectOwner (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Metodo GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
