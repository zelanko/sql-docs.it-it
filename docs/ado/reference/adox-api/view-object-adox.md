---
description: Oggetto View (ADOX)
title: Oggetto View (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: rothja
ms.author: jroth
ms.openlocfilehash: b84873da0c4cacc12d624763b466786eaf1532ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769020"
---
# <a name="view-object-adox"></a>Oggetto View (ADOX)
Rappresenta un set filtrato di record o una tabella virtuale. Quando viene utilizzato insieme all'oggetto [comando](../ado-api/command-object-ado.md) ADO, l'oggetto **View** può essere utilizzato per aggiungere, eliminare o modificare le visualizzazioni.  
  
## <a name="remarks"></a>Commenti  
 Una vista è una tabella virtuale, creata da altre tabelle o viste di database. L'oggetto **visualizzazione** consente di creare una visualizzazione senza dover essere a conoscenza o utilizzare la sintassi "Create View" del provider.  
  
 Con le proprietà di un oggetto **visualizzazione** , è possibile:  
  
-   Identificare la vista con la proprietà [Name](./name-property-adox.md) .  
  
-   Specificare l'oggetto **comando** ADO che può essere utilizzato per aggiungere, eliminare o modificare viste con la proprietà [Command](./command-property-adox.md) .  
  
-   Restituisce informazioni sulla data con le proprietà [DateCreated](./datecreated-property-adox.md) e [DateModified](./datemodified-property-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto View](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di raccolte views e Fields (VB)](./views-and-fields-collections-example-vb.md)   
 [Esempio di metodo Append views (VB)](./views-append-method-example-vb.md)   
 [Raccolta views, esempio di proprietà CommandText (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Esempio di metodo Delete views (VB)](./views-delete-method-example-vb.md)   
 [Raccolta Views (ADOX)](./views-collection-adox.md)