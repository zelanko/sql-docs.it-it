---
title: Append (metodo) (User ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e56391357e7a11c47efdf0ffaf3c9ae9704d5db3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206235"
---
# <a name="append-method-adox-users"></a>Metodo Append (raccolta Users ADOX)
Aggiunge un nuovo [utente](../../../ado/reference/adox-api/user-object-adox.md) dell'oggetto per il [utenti](../../../ado/reference/adox-api/users-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Utente*  
 Oggetto **Variant** valore contenente il **utente** oggetto da accodare o il nome dell'utente per creare e aggiungere.  
  
 *Password*  
 Facoltativo. Oggetto **stringa** valore contenente la password per l'utente. Il *Password* parametro corrisponde al valore specificato per il [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) metodo di un **utente** oggetto.  
  
## <a name="remarks"></a>Note  
 Il **gli utenti** raccolta di un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta gli utenti del catalogo. Il **gli utenti** raccolta per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti che hanno l'appartenenza a un gruppo specifico.  
  
 Se il provider non supporta la creazione di utenti, si verificherà un errore.  
  
> [!NOTE]
>  Prima di accodare un **utente** dell'oggetto per il **utenti** raccolta di un **gruppo** oggetto, un **utente** oggetto con lo stesso [nome ](../../../ado/reference/adox-api/name-property-adox.md) dell'oggetto da aggiungere deve già esistere nel **gli utenti** insieme del **catalogo**.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere utenti e gruppi, esempio di metodi ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Group ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (metodo) (oggetti Index ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti procedure ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
