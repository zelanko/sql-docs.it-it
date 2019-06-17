---
title: Gruppi di raccolta (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e0fe23c41f6a22a05e6a4c1d61f94a357f3c28c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706675"
---
# <a name="groups-collection-adox"></a>Raccolta di Groups (ADOX)
Contiene tutti archiviati [gruppo](../../../ado/reference/adox-api/group-object-adox.md) gli oggetti di un catalogo o un utente.  
  
## <a name="remarks"></a>Note  
 Il **gruppi** raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. Il **gruppi** raccolta per un [utente](../../../ado/reference/adox-api/user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Il [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) metodo per un **gruppi** raccolta sia univoca per ADOX. È possibile effettuare le operazioni seguenti:  
  
-   Aggiungere un nuovo gruppo di sicurezza alla raccolta con il **Append** (metodo).  
  
 Le proprietà e metodi restanti sono standard per le raccolte di ADO. È possibile effettuare le operazioni seguenti:  
  
-   Accedere a un gruppo di nell'insieme con il [elemento](../../../ado/reference/ado-api/item-property-ado.md) proprietà.  
  
-   Restituisce il numero di gruppi contenuti nella raccolta con il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà.  
  
-   Rimuovere un gruppo dalla raccolta con il [eliminare](../../../ado/reference/adox-api/delete-method-adox-collections.md) (metodo).  
  
-   Aggiornare gli oggetti nella raccolta in modo da riflettere lo schema del database corrente con il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) (metodo).  
  
> [!NOTE]
>  Prima di accodare un **gruppo** dell'oggetto per il **gruppi** raccolta di un **utente** oggetto, un **gruppo** oggetto con lo stesso [ Nome](../../../ado/reference/adox-api/name-property-adox.md) dell'oggetto da aggiungere deve già esistere nel **gruppi** insieme del **catalogo**.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti Group](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
