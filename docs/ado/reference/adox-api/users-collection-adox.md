---
title: Raccolta degli utenti (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964958"
---
# <a name="users-collection-adox"></a>Raccolta Users (ADOX)
Contiene tutti archiviati [utente](../../../ado/reference/adox-api/user-object-adox.md) gli oggetti di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) oppure [gruppo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Note  
 Il **gli utenti** raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta gli utenti del catalogo. Il **gli utenti** raccolta per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti che hanno l'appartenenza a un gruppo specifico.  
  
 Il [Append](../../../ado/reference/adox-api/append-method-adox-users.md) metodo per un **utenti** raccolta sia univoca per ADOX. È possibile:  
  
-   Aggiungere un nuovo utente alla raccolta utilizzando il **Append** (metodo).  
  
 Le proprietà e metodi restanti sono standard per le raccolte di ADO. È possibile:  
  
-   Accedere a un utente nella raccolta con il [elemento](../../../ado/reference/ado-api/item-property-ado.md) proprietà.  
  
-   Restituisce il numero di utenti inclusi nella raccolta con il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà.  
  
-   Rimuovere un utente dalla raccolta con il [eliminare](../../../ado/reference/adox-api/delete-method-adox-collections.md) (metodo).  
  
-   Aggiornare gli oggetti nella raccolta in base allo schema del database corrente con il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) (metodo).  
  
> [!NOTE]
>  Prima di accodare un **utente** dell'oggetto per il **utenti** raccolta di un **gruppo** oggetto, un **utente** oggetto con lo stesso [nome ](../../../ado/reference/adox-api/name-property-adox.md) dell'oggetto da aggiungere deve già esistere nel **gli utenti** insieme del **catalogo**.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti User](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [GetPermissions e SetPermissions metodi (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
