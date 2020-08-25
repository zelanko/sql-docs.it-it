---
description: Metodo SetObjectOwner
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
author: rothja
ms.author: jroth
ms.openlocfilehash: acefd94f29b030a6bee724686e11023a354d8921
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769410"
---
# <a name="setobjectowner-method"></a>Metodo SetObjectOwner
Specifica il proprietario di un oggetto in un [Catalogo](./catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parametri  
 *ObjectName*  
 Valore **stringa** che specifica il nome dell'oggetto per il quale specificare il proprietario.  
  
 *ObjectType*  
 Valore **Long** che può essere una delle costanti [ObjectTypeEnum](./objecttypeenum.md) che specifica il tipo di proprietario.  
  
 *OwnerName*  
 Valore **stringa** che specifica il [nome](./name-property-adox.md) dell' [utente](./user-object-adox.md) o del [gruppo](./group-object-adox.md) per il proprietario dell'oggetto.  
  
 *ObjectTypeId*  
 Facoltativa. Valore **Variant** che specifica il GUID per un tipo di oggetto provider non definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostato su **adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Commenti  
 Si verificherà un errore se il provider non supporta la specifica di proprietari di oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetObjectOwner e SetObjectOwner (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Metodo GetObjectOwner (ADOX)](./getobjectowner-method-adox.md)