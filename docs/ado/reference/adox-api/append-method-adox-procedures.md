---
title: Metodo Append (routine ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd64ba8119db1ecf2d2b621cd202c9f700b53475
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967289"
---
# <a name="append-method-adox-procedures"></a>Metodo Append (raccolta Procedures ADOX)
Aggiunge un nuovo oggetto [procedura](../../../ado/reference/adox-api/procedure-object-adox.md) alla raccolta [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 Valore **stringa** che specifica il nome della procedura da creare e accodare.  
  
 *Comando*  
 Oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO che rappresenta la routine da creare e accodare.  
  
## <a name="remarks"></a>Osservazioni  
 Crea una nuova stored procedure nell'origine dati con il nome e gli attributi specificati nell'oggetto **Command** .  
  
 Se il testo del comando specificato dall'utente rappresenta una vista anziché una routine, il comportamento dipende dal provider in uso. L' **Accodamento** avrà esito negativo se il provider non supporta la persistenza dei comandi.  
  
> [!NOTE]
>  Quando si usa il provider di OLE DB per Microsoft Jet, il metodo **Append** della raccolta **Procedures** consente di specificare una **vista** anziché una **routine** nel parametro *Command* . La **vista** verrà aggiunta all'origine dati e verrà aggiunta alla raccolta **Procedures** . Dopo l' **Accodamento**, se le raccolte **procedure** e **viste** vengono aggiornate, la **vista** non sarà più presente nella raccolta **Procedures** e verrà visualizzata nella raccolta **views** .  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append di procedure (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
