---
title: Oggetto (ADOX) gruppo | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966216"
---
# <a name="group-object-adox"></a>Oggetto Group (ADOX)
Rappresenta un account di gruppo che dispone delle autorizzazioni di accesso all'interno di un database protetto.  
  
## <a name="remarks"></a>Note  
 Il [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta gli account di gruppo del catalogo. Il **gruppi** raccolta per un [utente](../../../ado/reference/adox-api/user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Con la proprietà, le raccolte e i metodi di una **gruppo** dell'oggetto, è possibile:  
  
-   Identificare il gruppo con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Determinare se un gruppo dispone di lettura, scrittura o eliminazione delle autorizzazioni con il [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) metodi.  
  
-   Accesso agli account utente con le appartenenze nel gruppo con il [utenti](../../../ado/reference/adox-api/users-collection-adox.md) raccolta.  
  
-   Accedere alle proprietà specifiche del provider con il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Group](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta di gruppi (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
