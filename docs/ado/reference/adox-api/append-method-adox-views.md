---
title: Metodo Append (viste ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
author: rothja
ms.author: jroth
ms.openlocfilehash: 540ff52141139f4748cb2cd4c8979f5f8b55b230
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764002"
---
# <a name="append-method-adox-views"></a>Metodo Append (raccolta Views ADOX)
Crea un nuovo oggetto [visualizzazione](../../../ado/reference/adox-api/view-object-adox.md) e lo aggiunge alla raccolta [views](../../../ado/reference/adox-api/views-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 Valore **stringa** che specifica il nome della visualizzazione da creare.  
  
 *Comando*  
 Oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO che rappresenta la visualizzazione da creare.  
  
## <a name="remarks"></a>Commenti  
 Crea una nuova visualizzazione nell'origine dati con il nome e gli attributi specificati nell'oggetto **comando** .  
  
 Se il testo del comando specificato dall'utente rappresenta una procedura anziché una vista, il comportamento dipende dal provider. L' **Accodamento** avrà esito negativo se il provider non supporta la persistenza dei comandi.  
  
> [!NOTE]
>  Quando si usa il provider di OLE DB per Microsoft Jet, il metodo **Append** della raccolta **views** consente di specificare una **procedura** anziché una **vista** nel parametro *Command* . La **procedura** verrà aggiunta all'origine dati e verrà aggiunta alla raccolta **views** . Dopo l' **Accodamento**, se le raccolte **procedure** e **viste** vengono aggiornate, la **procedura** non sarà più presente nella raccolta **views** e verrà visualizzata nella raccolta **Procedures** .  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (oggetti User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
