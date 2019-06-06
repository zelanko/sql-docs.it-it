---
title: Metodo ChangePassword (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 981f2e5b801cd35b0aedb04e5f1aa11b741e4535
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708010"
---
# <a name="changepassword-method-adox"></a>Metodo ChangePassword (ADOX)
Modifica la password per un [utente](../../../ado/reference/adox-api/user-object-adox.md) account.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parametri  
 *OldPassword*  
 Oggetto **stringa** valore che specifica la password dell'utente esistente. Se l'utente non dispone di una password, usare una stringa vuota ("") per *OldPassword*.  
  
 *NewPassword*  
 Oggetto **stringa** valore che specifica la nuova password.  
  
## <a name="remarks"></a>Note  
 Per motivi di sicurezza, è necessario specificare la vecchia password oltre la nuova password.  
  
 Se il provider non supporta l'amministrazione delle proprietà di dominio trusted, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Append oggetti Group e User, esempio di metodi ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
