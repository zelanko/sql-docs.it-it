---
description: Raccolta Keys (ADOX)
title: Raccolta Keys (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 95d1b5b927f03a0592f25cc4cc79c0ffe78cee74
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770060"
---
# <a name="keys-collection-adox"></a>Raccolta Keys (ADOX)
Contiene tutti gli oggetti [chiave](./key-object-adox.md) di una [tabella](./table-object-adox.md).  
  
## <a name="remarks"></a>Commenti  
 Il metodo [Append](./append-method-adox-keys.md) per una [raccolta di chiavi]() è univoco per ADOX. È possibile:  
  
-   Aggiungere una nuova chiave alla raccolta con il metodo [Append](./append-method-adox-keys.md) .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile:  
  
-   Accedere a una chiave nella raccolta con la proprietà [Item](../ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di chiavi contenute nella raccolta con la proprietà [count](../ado-api/count-property-ado.md) .  
  
-   Rimuovere una chiave dalla raccolta con il metodo [Delete](./delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Proprietà, metodi ed eventi della raccolta Keys](./keys-collection-properties-methods-and-events.md)   
 [Oggetto Key (ADOX)](./key-object-adox.md)