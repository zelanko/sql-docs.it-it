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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c9892ddc3be28e63dae0f3f6440cc4a668498e3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764908"
---
# <a name="getobjectowner-method-adox"></a>Metodo GetObjectOwner (ADOX)
Restituisce il proprietario di un oggetto in un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **stringa** che specifica il [nome](../../../ado/reference/adox-api/name-property-adox.md) dell' [utente](../../../ado/reference/adox-api/user-object-adox.md) o del [gruppo](../../../ado/reference/adox-api/group-object-adox.md) a cui appartiene l'oggetto.  
  
#### <a name="parameters"></a>Parametri  
 *ObjectName*  
 Valore **stringa** che specifica il nome dell'oggetto per il quale restituire il proprietario.  
  
 *ObjectType*  
 Valore **Long** che può essere una delle costanti [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , che specifica il tipo dell'oggetto per il quale ottenere il proprietario.  
  
 *ObjectTypeId*  
 Facoltativa. Valore **Variant** che specifica il GUID per un tipo di oggetto provider non definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostato su **adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Commenti  
 Se il provider non supporta la restituzione di proprietari di oggetti, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetObjectOwner e SetObjectOwner (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Metodo SetObjectOwner (ADOX)](../../../ado/reference/adox-api/setobjectowner-method.md)
