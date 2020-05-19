---
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
ms.openlocfilehash: 1a7bebc1c05ab195d3b23c5c0894d4fcce967625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746546"
---
# <a name="keys-collection-adox"></a>Raccolta Keys (ADOX)
Contiene tutti gli oggetti [chiave](../../../ado/reference/adox-api/key-object-adox.md) di una [tabella](../../../ado/reference/adox-api/table-object-adox.md).  
  
## <a name="remarks"></a>Commenti  
 Il metodo [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) per una [raccolta di chiavi](../../../ado/reference/adox-api/keys-collection-adox.md) è univoco per ADOX. È possibile scegliere:  
  
-   Aggiungere una nuova chiave alla raccolta con il metodo [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile scegliere:  
  
-   Accedere a una chiave nella raccolta con la proprietà [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di chiavi contenute nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Rimuovere una chiave dalla raccolta con il metodo [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti Index](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Proprietà, metodi ed eventi della raccolta Keys](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [Oggetto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
