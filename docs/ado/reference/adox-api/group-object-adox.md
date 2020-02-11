---
title: Oggetto Group (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b4b3de5f445ddd09bf7d069b0b93d82c6f8de978
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966216"
---
# <a name="group-object-adox"></a>Oggetto Group (ADOX)
Rappresenta un account di gruppo che dispone di autorizzazioni di accesso all'interno di un database protetto.  
  
## <a name="remarks"></a>Osservazioni  
 La raccolta di [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. La raccolta **gruppi** per un [utente](../../../ado/reference/adox-api/user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Con le proprietà, le raccolte e i metodi di un oggetto **gruppo** , è possibile:  
  
-   Identificare il gruppo con la proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determinare se un gruppo dispone di autorizzazioni di lettura, scrittura o eliminazione con i metodi [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [sepermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Accedere agli account utente che dispongono di appartenenze al gruppo con la raccolta [Users](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
-   Accedere alle proprietà specifiche del provider con la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Group](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
