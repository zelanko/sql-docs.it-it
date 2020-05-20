---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: rothja
ms.author: jroth
ms.openlocfilehash: d493218f31965c04b5a64321c4a1bf87a2518f6f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763792"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Specifica il tipo di oggetto di database per il quale impostare le autorizzazioni o la proprietà.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|L'oggetto è una colonna.|  
|**adPermObjDatabase**|3|L'oggetto è un database.|  
|**adPermObjProcedure**|4|L'oggetto è una routine.|  
|**adPermObjProviderSpecific**|-1|L'oggetto è un tipo definito dal provider. Si verificherà un errore se il parametro *ObjectType* è **adPermObjProviderSpecific** e non viene fornito un *ObjectTypeId* .|  
|**adPermObjTable**|1|L'oggetto è una tabella.|  
|**adPermObjView**|5|L'oggetto è una vista.|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[Metodo GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[Metodo SetObjectOwner (ADOX)](../../../ado/reference/adox-api/setobjectowner-method.md)|[Metodo SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
