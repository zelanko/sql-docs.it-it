---
title: Append (metodo) (View ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f5f58ff2f38ff80d90750901b8943efc00f389c6
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718951"
---
# <a name="append-method-adox-views"></a>Metodo Append (raccolta Views ADOX)
Crea un nuovo [View](../../../ado/reference/adox-api/view-object-adox.md) dell'oggetto e lo aggiunge al [viste](../../../ado/reference/adox-api/views-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parametri  
 *Name*  
 Oggetto **stringa** valore che specifica il nome della visualizzazione da creare.  
  
 *Command*  
 Un oggetto ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto che rappresenta la visualizzazione da creare.  
  
## <a name="remarks"></a>Note  
 Crea una nuova visualizzazione nell'origine dati con il nome e gli attributi specificati nel **comando** oggetto.  
  
 Se il testo del comando specificato dall'utente rappresenta una procedura anziché una vista, il comportamento è dipende dal provider. **Accodare** avrà esito negativo se il provider non supporta comandi di persistenza.  
  
> [!NOTE]
>  Quando si usa il Provider OLE DB per Microsoft Jet, il **viste** insieme **Append** metodo consentirà di specificare una **Procedure** anziché un **vista**  nella *comando* parametro. Il **routine** verrà aggiunto all'origine dati e verrà aggiunto al **viste** raccolta. Dopo il **Append**, se il **procedure** e **viste** raccolte vengono aggiornate, il **procedura** non saranno nel **Viste** raccolta e verrà visualizzato nei **procedure** raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di esempio del metodo Append (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Group ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (metodo) (oggetti Index ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti procedure ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (oggetti User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)
