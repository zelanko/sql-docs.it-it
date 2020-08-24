---
description: Oggetto Procedure (ADOX)
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
ms.openlocfilehash: 8932d2b71f631f24a9ce825804074b9094f932b9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769710"
---
# <a name="procedure-object-adox"></a>Oggetto Procedure (ADOX)
Rappresenta un stored procedure. Quando viene utilizzato insieme all'oggetto [comando](../ado-api/command-object-ado.md) ADO, è possibile utilizzare l'oggetto **procedura** per l'aggiunta, l'eliminazione o la modifica di stored procedure.  
  
## <a name="remarks"></a>Commenti  
 L'oggetto **procedura** consente di creare un stored procedure senza dover essere a conoscenza o utilizzare la sintassi "create procedure" del provider.  
  
 Con le proprietà di un oggetto **procedura** , è possibile:  
  
-   Identificare la procedura con la proprietà [Name](./name-property-adox.md) .  
  
-   Specificare l'oggetto **comando** ADO che può essere utilizzato per creare o eseguire la procedura con la proprietà [Command](./command-property-adox.md) .  
  
-   Restituisce informazioni sulla data con le proprietà [DateCreated](./datecreated-property-adox.md) e [DateModified](./datemodified-property-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Procedure](./procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Command e CommandText (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Raccolta Parameters, esempio di proprietà Command (VB)](./parameters-collection-command-property-example-vb.md)   
 [Esempio di metodo Append di procedure (VB)](./procedures-append-method-example-vb.md)   
 [Esempio di metodo Delete delle procedure (VB)](./procedures-delete-method-example-vb.md)   
 [Raccolta Procedures (ADOX)](./procedures-collection-adox.md)