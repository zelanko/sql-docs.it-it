---
title: Visualizzare oggetti (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61b3f81a23c3bb35921e0374eea44e58a31dcd4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281289"
---
# <a name="view-object-adox"></a>Oggetto View (ADOX)
Rappresenta un set filtrato di record o una tabella virtuale. Quando usato in combinazione con l'oggetto ADO [comandi](../../../ado/reference/ado-api/command-object-ado.md) oggetto, il **visualizzazione** oggetto può essere utilizzato per l'aggiunta, eliminazione o modifica di viste.  
  
## <a name="remarks"></a>Note  
 Una vista è una tabella virtuale, creata dal database tabelle o viste. Il **vista** oggetto consente di creare una visualizzazione senza la necessità di conoscere o usare la sintassi "CREATE VIEW" del provider.  
  
 Con le proprietà di un **vista** dell'oggetto, è possibile:  
  
-   Identificare la vista con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Specificare l'oggetto ADO **comandi** oggetto che può essere utilizzato per aggiungere, eliminare o modificare le viste con la [comando](../../../ado/reference/adox-api/command-property-adox.md) proprietà.  
  
-   Restituisce informazioni sulle date con il [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) proprietà.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto View](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Viste e esempio di raccolte di campi (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Viste di esempio del metodo Append (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Raccolta di oggetti View, esempio di proprietà CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Viste di esempio del metodo Delete (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
