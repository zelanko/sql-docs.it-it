---
title: Indice di oggetto (ADOX) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: b6fd63de0b6147b86aa0d6b548669c56aefdcf20
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706712"
---
# <a name="index-object-adox"></a>Oggetto Index (ADOX)
Rappresenta un indice di una tabella di database.  
  
## <a name="remarks"></a>Note  
 Il codice seguente crea una nuova **indice**:  
  
```  
Dim obj As New Index  
```  
  
 Con le proprietà e raccolte di un' **indice** dell'oggetto, è possibile:  
  
-   Identificare l'indice con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Accedere alle colonne del database dell'indice con il [colonne](../../../ado/reference/adox-api/columns-collection-adox.md) raccolta.  
  
-   Specificare se le chiavi di indice devono essere univoche con il [Unique](../../../ado/reference/adox-api/unique-property-adox.md) proprietà.  
  
-   Specificare se l'indice è la chiave primaria per una tabella con il [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) proprietà.  
  
-   Specificare se i record con valori null nei relativi campi di indice presentano le voci di indice con il [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) proprietà.  
  
-   Specificare se l'indice è in cluster con il [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) proprietà.  
  
-   Accedere alle proprietà di indice specifico del provider con il [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
> [!NOTE]
>  Si verifica un errore quando si aggiunge un [colonna](../../../ado/reference/adox-api/column-object-adox.md) per il **colonne** raccolta di un **indice** se il **colonna** non esiste in un [Nella tabella](../../../ado/reference/adox-api/table-object-adox.md) oggetto già accodato per il [tabelle](../../../ado/reference/adox-api/tables-collection-adox.md) raccolta.  
  
> [!NOTE]
>  Il provider di dati non supportino tutte le proprietà del **indice** oggetti. Se è stato impostato un valore per una proprietà che non è supportato dal provider, si verificherà un errore. Per ottenere nuove **indice** oggetti, l'errore si verifica quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verifica quando l'impostazione della proprietà.  
  
> [!NOTE]
>  Durante la creazione **indice** oggetti, l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporta la proprietà. Per altre informazioni sulle proprietà che supporta il provider, vedere la documentazione del provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo (VB) Append](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Esempio di proprietà IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [Esempio PrimaryKey e proprietà univoche (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta di indici (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
