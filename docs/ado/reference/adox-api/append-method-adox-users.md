---
title: Metodo Append (utenti ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c010b291468432544a037d15fbaa790fc3ee789d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764022"
---
# <a name="append-method-adox-users"></a>Metodo Append (raccolta Users ADOX)
Aggiunge un nuovo oggetto [utente](../../../ado/reference/adox-api/user-object-adox.md) alla raccolta [Users](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Utente*  
 Valore **Variant** che contiene l'oggetto **utente** da accodare o il nome dell'utente da creare e accodare.  
  
 *Password*  
 Facoltativa. Valore **stringa** che contiene la password per l'utente. Il parametro *password* corrisponde al valore specificato dal metodo [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) di un oggetto **utente** .  
  
## <a name="remarks"></a>Commenti  
 La raccolta **Users** di un [Catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) rappresenta tutti gli utenti del catalogo. La raccolta **Users** per un [gruppo](../../../ado/reference/adox-api/group-object-adox.md) rappresenta solo gli utenti che dispongono di un'appartenenza al gruppo specifico.  
  
 Se il provider non supporta la creazione di utenti, si verificherà un errore.  
  
> [!NOTE]
>  Prima di aggiungere un oggetto **utente** alla raccolta **Users** di un oggetto **gruppo** , deve esistere già un oggetto **utente** con lo stesso [nome](../../../ado/reference/adox-api/name-property-adox.md) di quello da accodare nella raccolta **Users** del **Catalogo**.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Accodamento di gruppi e utenti, esempio di Metodi ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
