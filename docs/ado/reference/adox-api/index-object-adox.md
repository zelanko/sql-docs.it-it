---
title: Oggetto index (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7bff462b7c9ffe115cdfd52d1ec1f0a810a50531
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966087"
---
# <a name="index-object-adox"></a>Oggetto Index (ADOX)
Rappresenta un indice di una tabella di database.  
  
## <a name="remarks"></a>Osservazioni  
 Il codice seguente crea un nuovo **Indice**:  
  
```  
Dim obj As New Index  
```  
  
 Con le proprietà e le raccolte di un oggetto **index** è possibile:  
  
-   Identificare l'indice con la proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Accedere alle colonne del database dell'indice con la raccolta [Columns](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Consente di specificare se le chiavi dell'indice devono essere univoche con la proprietà [Unique](../../../ado/reference/adox-api/unique-property-adox.md) .  
  
-   Consente di specificare se l'indice è la chiave primaria di una tabella con la proprietà [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) .  
  
-   Consente di specificare se i record con valori null nei rispettivi campi di indice hanno voci di indice con la proprietà [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) .  
  
-   Consente di specificare se l'indice è in cluster con la proprietà [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) .  
  
-   Accedere alle proprietà di indice specifiche del provider con la raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Si verificherà un errore durante l'aggiunta di una [colonna](../../../ado/reference/adox-api/column-object-adox.md) alla raccolta **Columns** di un **Indice** se la **colonna** non esiste in un oggetto [Table](../../../ado/reference/adox-api/table-object-adox.md) già accodato alla raccolta [Tables](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
> [!NOTE]
>  Il provider di dati potrebbe non supportare tutte le proprietà degli oggetti **Indice** . Se è stato impostato un valore per una proprietà non supportata dal provider, si verificherà un errore. Per i nuovi oggetti **index** , l'errore si verificherà quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verificherà quando si imposta la proprietà.  
  
> [!NOTE]
>  Quando si creano oggetti **index** , l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporti la proprietà. Per ulteriori informazioni sulle proprietà supportate dal provider, vedere la documentazione del provider.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append degli indici (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Esempio di proprietà IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [Esempio di proprietà PrimaryKey e Unique (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
