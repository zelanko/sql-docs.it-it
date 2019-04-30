---
title: Append (metodo) (oggetti procedure ADOX) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 348b2876e4293ad912383859ace47e462da31bcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207189"
---
# <a name="append-method-adox-procedures"></a>Metodo Append (raccolta Procedures ADOX)
Aggiunge un nuovo [routine](../../../ado/reference/adox-api/procedure-object-adox.md) dell'oggetto per il [procedure](../../../ado/reference/adox-api/procedures-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parametri  
 *Name*  
 Oggetto **stringa** valore che specifica il nome della procedura per creare e di aggiunta.  
  
 *Command*  
 Un oggetto ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) oggetto che rappresenta la procedura per creare e aggiungere.  
  
## <a name="remarks"></a>Note  
 Crea una nuova stored procedure nell'origine dati con il nome e gli attributi specificati nel **comando** oggetto.  
  
 Se il testo del comando specificato dall'utente rappresenta una vista anziché una routine, il comportamento è dipendente da provider in uso. **Accodare** avrà esito negativo se il provider non supporta comandi di persistenza.  
  
> [!NOTE]
>  Quando si usa il Provider OLE DB per Microsoft Jet, il **procedure** insieme **Append** metodo consentirà di specificare una **visualizzazione** anziché un  **Routine** nella *comando* parametro. Il **View** verrà aggiunto all'origine dati e verrà aggiunto al **procedure** raccolta. Dopo il **Append**, se il **procedure** e **viste** raccolte vengono aggiornate, il **visualizzazione** non saranno nel **Procedure** raccolta e verrà visualizzato nei **viste** raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure di esempio del metodo Append (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Group ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (metodo) (oggetti Index ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (metodo) (User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
