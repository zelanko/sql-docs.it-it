---
title: Tabella oggetti (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 43679897bf49e9a2505dad1540f3b494b66f180d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705856"
---
# <a name="table-object-adox"></a>Oggetto Table (ADOX)
Rappresenta una tabella di database, incluse le colonne, indici e chiavi.  
  
## <a name="remarks"></a>Note  
 Il codice seguente crea una nuova **tabella**:  
  
```  
Dim obj As New Table  
```  
  
 Con le proprietà e raccolte di un **tabella** dell'oggetto, è possibile:  
  
-   Identificare la tabella con il [nome proprietà (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Determinare il tipo di tabella con il [proprietà Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) proprietà.  
  
-   Accedere alle colonne del database della tabella con il [raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) raccolta.  
  
-   Accedere gli indici della tabella con il [raccolta di indici (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Accesso alle chiavi della tabella con il [raccolta di chiavi (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Specificare il catalogo cui appartiene la tabella con il [proprietà ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) proprietà.  
  
-   Restituisce informazioni sulle date con il [proprietà DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) e [proprietà DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) proprietà.  
  
-   Accedere alle proprietà di tabella specifico del provider con il [raccolta di proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
> [!NOTE]
>  Il provider di dati non supportino tutte le proprietà del **tabella** oggetti. Se è stato impostato un valore per una proprietà che non supporta il provider, si verificherà un errore. Per ottenere nuove **tabella** oggetti, l'errore si verifica quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verifica quando l'impostazione della proprietà.  
>   
>  Durante la creazione **tabella** oggetti, l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporta la proprietà. Per altre informazioni sulle proprietà che supporta il provider, vedere la documentazione del provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection di Catalog (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Tabelle e colonne aggiungere metodi, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo Connection Close, esempio di proprietà Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta di indici (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
