---
title: Oggetto procedure (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a56088e47a9f794f1862ef87bf142a8d3ab12c4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763692"
---
# <a name="procedure-object-adox"></a>Oggetto Procedure (ADOX)
Rappresenta un stored procedure. Quando viene utilizzato insieme all'oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO, è possibile utilizzare l'oggetto **procedura** per l'aggiunta, l'eliminazione o la modifica di stored procedure.  
  
## <a name="remarks"></a>Osservazioni  
 L'oggetto **procedura** consente di creare un stored procedure senza dover essere a conoscenza o utilizzare la sintassi "create procedure" del provider.  
  
 Con le proprietà di un oggetto **procedura** , è possibile:  
  
-   Identificare la procedura con la proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Specificare l'oggetto **comando** ADO che può essere utilizzato per creare o eseguire la procedura con la proprietà [Command](../../../ado/reference/adox-api/command-property-adox.md) .  
  
-   Restituisce informazioni sulla data con le proprietà [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Procedure](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Command e CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Raccolta Parameters, esempio di proprietà Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Esempio di metodo Append di procedure (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Esempio di metodo Delete delle procedure (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
