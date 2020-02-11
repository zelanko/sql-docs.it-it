---
title: Raccolta views (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cec2462f8726e7c580a7d6755394c6c3f07c85b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964775"
---
# <a name="views-collection-adox"></a>Raccolta Views (ADOX)
Contiene tutti gli oggetti di [visualizzazione](../../../ado/reference/adox-api/view-object-adox.md) di un catalogo.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo [Append](../../../ado/reference/adox-api/append-method-adox-views.md) per una raccolta **views** è univoco per ADOX. È possibile:  
  
-   Aggiungere una nuova vista alla raccolta con il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile:  
  
-   Accedere a una vista della raccolta con la proprietà [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di visualizzazioni contenute nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Rimuovere una vista dalla raccolta con il metodo [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta Views](../../../ado/reference/adox-api/views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di raccolte views e Fields (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Esempio di metodo Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Raccolta views, esempio di proprietà CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Esempio di metodo Delete views (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Esempio di metodo Refresh views (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)
