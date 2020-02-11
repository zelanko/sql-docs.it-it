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
ms.openlocfilehash: de8baf504a76407037322fd6b799f6d63584eae7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967032"
---
# <a name="changepassword-method-adox"></a>Metodo ChangePassword (ADOX)
Modifica la password per un account [utente](../../../ado/reference/adox-api/user-object-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parametri  
 *OldPassword*  
 Valore **stringa** che specifica la password esistente dell'utente. Se l'utente non dispone attualmente di una password, utilizzare una stringa vuota ("") per *oldPassword*.  
  
 *NewPassword*  
 Valore **stringa** che specifica la nuova password.  
  
## <a name="remarks"></a>Osservazioni  
 Per motivi di sicurezza, è necessario specificare la vecchia password oltre alla nuova password.  
  
 Si verificherà un errore se il provider non supporta l'amministrazione delle proprietà del trustee.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio dei metodi Append di Groups e Users e del metodo ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
