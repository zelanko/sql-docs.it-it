---
title: Oggetto User (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: 55315ab64f87c6aba1c988c752c4e21811fef35c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762712"
---
# <a name="user-object-adox"></a>Oggetto User (ADOX)
Rappresenta un account utente che dispone di autorizzazioni di accesso all'interno di un database protetto.  
  
## <a name="remarks"></a>Osservazioni  
 La raccolta [Users](../../../ado/reference/adox-api/users-collection-adox.md) di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli utenti del catalogo. La raccolta **Users** per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti del gruppo specifico.  
  
 Con le proprietà, le raccolte e i metodi di un oggetto **utente** , è possibile:  
  
-   Identificare l'utente con la proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Modificare la password per un utente con il metodo [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) .  
  
-   Determinare se un utente dispone di autorizzazioni di lettura, scrittura o eliminazione con i metodi [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [sepermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Accedere ai gruppi a cui appartiene un utente con la raccolta di [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
-   Accedere alle proprietà specifiche del provider con la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
-   Determinare il [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) per un utente.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetPermissions e sepermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Raccolta Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
