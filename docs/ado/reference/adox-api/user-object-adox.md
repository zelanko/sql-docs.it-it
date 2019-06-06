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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6fb3ebf1921bf0e61fe9d5a8dcf9fc2cd0dce6c1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705650"
---
# <a name="user-object-adox"></a>Oggetto User (ADOX)
Rappresenta un account utente che dispone delle autorizzazioni di accesso all'interno di un database protetto.  
  
## <a name="remarks"></a>Note  
 Il [gli utenti](../../../ado/reference/adox-api/users-collection-adox.md) raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta gli utenti del catalogo. Il **gli utenti** raccolta per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti del gruppo specifico.  
  
 Con la proprietà, le raccolte e i metodi di una **utente** dell'oggetto, è possibile:  
  
-   Identificare l'utente con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Modificare la password per un utente con il [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) (metodo).  
  
-   Determinare se un utente dispone di lettura, scrittura o eliminazione delle autorizzazioni con il [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) metodi.  
  
-   Accedere ai gruppi a cui appartiene un utente con il [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) raccolta.  
  
-   Accedere alle proprietà specifiche del provider con il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
-   Determinare il [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) per un utente.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [GetPermissions e SetPermissions metodi (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Raccolta di gruppi (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
