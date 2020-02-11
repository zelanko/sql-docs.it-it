---
title: Oggetto Column (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db2c2dbe6af2a50fc2507a9ade92d83e0502f2ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966918"
---
# <a name="column-object-adox"></a>Oggetto Column (ADOX)
Rappresenta una colonna di una tabella, un indice o una chiave.  
  
## <a name="remarks"></a>Osservazioni  
 Il codice seguente crea una nuova **colonna**:  
  
 `Dim obj As New Column`  
  
 Con le proprietà e le raccolte di un oggetto **colonna** è possibile:  
  
-   Identificare la colonna con la proprietà [Name Property (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Specificare il tipo di dati della colonna con la proprietà del [tipo (chiave) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) .  
  
-   Determinare se la colonna è a lunghezza fissa o se può contenere valori null con la proprietà [Attributes Property (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) .  
  
-   Specificare la dimensione massima della colonna con la proprietà [DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) .  
  
-   Per i valori di dati numerici, specificare la scala con la proprietà [NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) .  
  
-   Per valore di dati numerici, specificare la precisione massima con la proprietà [Precision Property (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) .  
  
-   Specificare l' [oggetto catalogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) proprietario della colonna con la proprietà [ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) .  
  
-   Per le colonne chiave, specificare il nome della colonna correlata nella tabella correlata con la proprietà [RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) .  
  
-   Per le colonne di indice, specificare se l'ordinamento è crescente o decrescente con la proprietà [SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) .  
  
-   Accedere alle proprietà specifiche del provider con la raccolta [Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Non tutte le proprietà degli oggetti **colonna** possono essere supportate dal provider di dati. Se è stato impostato un valore per una proprietà non supportata dal provider, si verificherà un errore. Per i nuovi oggetti **Column** , l'errore si verificherà quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verificherà quando si imposta la proprietà.  
>   
>  Quando si creano oggetti **Column** , l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporti la proprietà. Per ulteriori informazioni sulle proprietà supportate dal provider, vedere la documentazione del provider.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo di chiusura della connessione, esempio di proprietà del tipo di tabella (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di codice ADOX: esempio di proprietà NumericScale e Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
