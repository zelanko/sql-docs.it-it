---
description: Metodo ChangePassword (ADOX)
title: Metodo ChangePassword (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e51037f9838e9aef279351c822e6c35ffb25f0fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985202"
---
# <a name="changepassword-method-adox"></a>Metodo ChangePassword (ADOX)
Modifica la password per un account [utente](./user-object-adox.md) .  
  
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
 [Oggetto User (ADOX)](./user-object-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio dei metodi Append di Groups e Users e del metodo ChangePassword (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)