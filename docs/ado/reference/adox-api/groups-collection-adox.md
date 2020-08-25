---
description: Raccolta di Groups (ADOX)
title: Raccolta Groups (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5edecbbfebeea82d28f97bc31d15e04bf28c576a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770330"
---
# <a name="groups-collection-adox"></a>Raccolta di Groups (ADOX)
Contiene tutti gli oggetti [gruppo](./group-object-adox.md) archiviati di un catalogo o di un utente.  
  
## <a name="remarks"></a>Commenti  
 La raccolta di **gruppi** di un [Catalogo](./catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. La raccolta **gruppi** per un [utente](./user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Il metodo [Append](./append-method-adox-groups.md) per una raccolta di **gruppi** è univoco per ADOX. È possibile:  
  
-   Aggiungere un nuovo gruppo di sicurezza alla raccolta con il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile:  
  
-   Accedere a un gruppo della raccolta con la proprietà [Item](../ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di gruppi contenuti nella raccolta con la proprietà [count](../ado-api/count-property-ado.md) .  
  
-   Rimuovere un gruppo dalla raccolta con il metodo [Delete](./delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Prima di aggiungere un **oggetto gruppo** alla raccolta **di gruppi** di un oggetto **utente** , un oggetto **gruppo** con lo stesso [nome](./name-property-adox.md) di quello da accodare deve esistere già nella raccolta di **gruppi** del **Catalogo**.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta Groups](./groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Catalog (ADOX)](./catalog-object-adox.md)   
 [Oggetto Group (ADOX)](./group-object-adox.md)