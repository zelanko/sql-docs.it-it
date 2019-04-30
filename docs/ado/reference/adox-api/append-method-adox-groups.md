---
title: Append (metodo) (oggetti Group ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 171aaa250930d5563d8ce6ec3b08b5939710b881
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206352"
---
# <a name="append-method-adox-groups"></a>Metodo Append (raccolta Groups ADOX)
Aggiunge un nuovo [gruppo](../../../ado/reference/adox-api/group-object-adox.md) dell'oggetto per il [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parametri  
 *Gruppo*  
 Il **gruppo** il nome del gruppo per creare e aggiungere o oggetto da accodare.  
  
## <a name="remarks"></a>Note  
 Il **gruppi** raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. Il **gruppi** raccolta per un [utente](../../../ado/reference/adox-api/user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Se il provider non supporta la creazione di gruppi, si verificherà un errore.  
  
> [!NOTE]
>  Prima di accodare un **gruppo** dell'oggetto per il **gruppi** raccolta di un **utente** oggetto, un **gruppo** oggetto con lo stesso [ Nome](../../../ado/reference/adox-api/name-property-adox.md) dell'oggetto da aggiungere deve già esistere nel **gruppi** insieme del **catalogo**.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Group (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere utenti e gruppi, esempio di metodi ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Index ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti procedure ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (metodo) (User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
