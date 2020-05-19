---
title: Raccolta Users (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: rothja
ms.author: jroth
ms.openlocfilehash: 4befb68c861edee0f5c1423e86ee1fb21067c2a5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753175"
---
# <a name="users-collection-adox"></a>Raccolta Users (ADOX)
Contiene tutti gli oggetti [utente](../../../ado/reference/adox-api/user-object-adox.md) archiviati di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) o di un [gruppo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Osservazioni  
 La raccolta **Users** di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli utenti del catalogo. La raccolta **Users** per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti che dispongono di un'appartenenza al gruppo specifico.  
  
 Il metodo [Append](../../../ado/reference/adox-api/append-method-adox-users.md) per una raccolta **Users** è univoco per ADOX. È possibile scegliere:  
  
-   Aggiungere un nuovo utente alla raccolta usando il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile scegliere:  
  
-   Accedere a un utente nella raccolta con la proprietà [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di utenti contenuti nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Rimuovere un utente dalla raccolta con il metodo [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Prima di aggiungere un oggetto **utente** alla raccolta **Users** di un oggetto **gruppo** , deve esistere già un oggetto **utente** con lo stesso [nome](../../../ado/reference/adox-api/name-property-adox.md) di quello da accodare nella raccolta **Users** del **Catalogo**.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti User](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetPermissions e sepermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
