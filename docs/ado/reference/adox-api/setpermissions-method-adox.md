---
description: Metodo SetPermissions (ADOX)
title: Metodo sepermissions (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a13e1dc23556888c2d4ee5c013472614b764d57
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769400"
---
# <a name="setpermissions-method-adox"></a>Metodo SetPermissions (ADOX)
Specifica le autorizzazioni per un [gruppo](./group-object-adox.md) o un [utente](./user-object-adox.md) in un oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 Valore **stringa** che specifica il nome dell'oggetto per il quale impostare le autorizzazioni.  
  
 *ObjectType*  
 Valore **Long** che può essere una delle costanti [ObjectTypeEnum](./objecttypeenum.md) , che specifica il tipo dell'oggetto per il quale ottenere le autorizzazioni.  
  
 *Azione*  
 Valore **Long** che può essere una delle costanti [ActionEnum indicante](./actionenum.md) che specifica il tipo di azione da eseguire durante l'impostazione delle autorizzazioni.  
  
 *Diritti*  
 Valore **Long** che può essere una maschera di maschera di una o più costanti [RightsEnum](./rightsenum.md) , che indica i diritti da impostare.  
  
 *Ereditare*  
 Facoltativa. Valore **Long** che può essere una delle costanti [InheritTypeEnum](./inherittypeenum.md) , che specifica il modo in cui gli oggetti erediteranno tali autorizzazioni. Il valore predefinito è **adInheritNone**.  
  
 *ObjectTypeId*  
 Facoltativa. Valore **Variant** che specifica il GUID per un tipo di oggetto provider non definito dalla specifica OLE DB. Questo parametro è obbligatorio se *ObjectType* è impostato su **adPermObjProviderSpecific**; in caso contrario, non viene utilizzato.  
  
## <a name="remarks"></a>Commenti  
 Se il provider non supporta l'impostazione dei diritti di accesso per gruppi o utenti, si verificherà un errore.  
  
> [!NOTE]
>  Quando si richiamano le **autorizzazioni**, l'impostazione di Actions su **adAccessRevoke** esegue l'override di qualsiasi impostazione del parametro *Rights* . Non impostare *azioni* su **adAccessRevoke** se si desidera che i diritti specificati nel parametro *Rights* abbiano effetto.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Group (ADOX)](./group-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto User (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi GetPermissions e sepermissions (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Metodo GetPermissions (ADOX)](./getpermissions-method-adox.md)   
 [Proprietà Name (ADOX)](./name-property-adox.md)