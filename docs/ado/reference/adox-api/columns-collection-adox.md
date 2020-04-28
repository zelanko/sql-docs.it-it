---
title: Raccolta Columns (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc3686ac69d7afeeebec14939a42e073f796b1ec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966848"
---
# <a name="columns-collection-adox"></a>Raccolta Columns (ADOX)
Contiene tutti gli oggetti [colonna](../../../ado/reference/adox-api/column-object-adox.md) di una tabella, un indice o una chiave.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) per una raccolta **Columns** è univoco per ADOX. È possibile scegliere:  
  
-   Aggiungere una nuova colonna alla raccolta con il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile scegliere:  
  
-   Accedere a una colonna della raccolta con la proprietà [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di colonne contenute nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Rimuovere una colonna dalla raccolta con il metodo [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Si verificherà un errore durante l'aggiunta di una **colonna** alla raccolta **Columns** di un [Indice](../../../ado/reference/adox-api/index-object-adox.md) se la **colonna** non esiste in una [tabella](../../../ado/reference/adox-api/table-object-adox.md) già accodata alla raccolta [Tables](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti Column](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo di chiusura della connessione, esempio di proprietà del tipo di tabella (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
