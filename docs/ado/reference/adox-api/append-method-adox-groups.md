---
title: Metodo Append (gruppi ADOX) | Microsoft Docs
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
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967312"
---
# <a name="append-method-adox-groups"></a>Metodo Append (raccolta Groups ADOX)
Aggiunge un nuovo oggetto [gruppo](../../../ado/reference/adox-api/group-object-adox.md) alla raccolta di [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parametri  
 *Gruppo*  
 Oggetto **gruppo** da accodare o il nome del gruppo da creare e accodare.  
  
## <a name="remarks"></a>Osservazioni  
 La raccolta di **gruppi** di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli account di gruppo del catalogo. La raccolta **gruppi** per un [utente](../../../ado/reference/adox-api/user-object-adox.md) rappresenta solo il gruppo a cui appartiene l'utente.  
  
 Se il provider non supporta la creazione di gruppi, si verificherà un errore.  
  
> [!NOTE]
>  Prima di aggiungere un **oggetto gruppo** alla raccolta **di gruppi** di un oggetto **utente** , un oggetto **gruppo** con lo stesso [nome](../../../ado/reference/adox-api/name-property-adox.md) di quello da accodare deve esistere già nella raccolta di **gruppi** del **Catalogo**.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Group (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Accodamento di gruppi e utenti, esempio di Metodi ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
