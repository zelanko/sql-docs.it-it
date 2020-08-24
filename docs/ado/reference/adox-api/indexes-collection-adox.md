---
description: Raccolta Indexes (ADOX)
title: Raccolta Indexes (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: 0075ca8340d869f803a10d296672e03326c5bad6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770270"
---
# <a name="indexes-collection-adox"></a>Raccolta Indexes (ADOX)
Contiene tutti gli oggetti [Indice](./index-object-adox.md) di una tabella.  
  
## <a name="remarks"></a>Commenti  
 Il metodo [Append](./append-method-adox-indexes.md) per una raccolta **indexes** è univoco per ADOX. È possibile:  
  
-   Aggiungere un nuovo indice alla raccolta con il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile:  
  
-   Accedere a un indice nella raccolta con la proprietà [Item](../ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di indici contenuti nella raccolta con la proprietà [count](../ado-api/count-property-ado.md) .  
  
-   Rimuovere un indice dalla raccolta con il metodo [Delete](./delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append degli indici (VB)](./indexes-append-method-example-vb.md)   
 [Oggetto Index (ADOX)](./index-object-adox.md)