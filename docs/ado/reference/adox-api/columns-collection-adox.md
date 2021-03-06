---
description: Raccolta Columns (ADOX)
title: Raccolta Columns (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f1295aea12a1b9d60427864993630320d0f973ce
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985022"
---
# <a name="columns-collection-adox"></a>Raccolta Columns (ADOX)
Contiene tutti gli oggetti [colonna](./column-object-adox.md) di una tabella, un indice o una chiave.  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo [Append](./append-method-adox-columns.md) per una raccolta **Columns** è univoco per ADOX. È possibile:  
  
-   Aggiungere una nuova colonna alla raccolta con il metodo **Append** .  
  
 Le proprietà e i metodi rimanenti sono standard per le raccolte ADO. È possibile:  
  
-   Accedere a una colonna della raccolta con la proprietà [Item](../ado-api/item-property-ado.md) .  
  
-   Restituisce il numero di colonne contenute nella raccolta con la proprietà [count](../ado-api/count-property-ado.md) .  
  
-   Rimuovere una colonna dalla raccolta con il metodo [Delete](./delete-method-adox-collections.md) .  
  
-   Aggiornare gli oggetti della raccolta in modo che corrispondano allo schema del database corrente con il metodo [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Si verificherà un errore durante l'aggiunta di una **colonna** alla raccolta **Columns** di un [Indice](./index-object-adox.md) se la **colonna** non esiste in una [tabella](./table-object-adox.md) già accodata alla raccolta [Tables](./tables-collection-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi della raccolta Columns](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo di chiusura della connessione, esempio di proprietà del tipo di tabella (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Oggetto Column (ADOX)](./column-object-adox.md)