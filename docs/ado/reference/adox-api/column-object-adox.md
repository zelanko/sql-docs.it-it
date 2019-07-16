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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966918"
---
# <a name="column-object-adox"></a>Oggetto Column (ADOX)
Rappresenta una colonna da una tabella, indice o chiave.  
  
## <a name="remarks"></a>Note  
 Il codice seguente crea una nuova **colonna**:  
  
 `Dim obj As New Column`  
  
 Con le proprietà e raccolte di un **colonna** dell'oggetto, è possibile:  
  
-   Identificare la colonna con il [nome proprietà (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Specificare il tipo di dati della colonna con il [proprietà del tipo (chiave) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) proprietà.  
  
-   Determinare se la colonna è a lunghezza fissa o se può contenere valori null con il [proprietà attributi (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) proprietà.  
  
-   Specificare le dimensioni massime della colonna con il [proprietà DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) proprietà.  
  
-   Per i valori di dati numerici, di specificare la scala con le [proprietà NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) proprietà.  
  
-   Per il valore di dati numerico, specificare la precisione massima con il [proprietà Precision (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) proprietà.  
  
-   Specificare il [oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) cui appartiene la colonna con il [proprietà ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) proprietà.  
  
-   Per le colonne chiave, specificare il nome della colonna correlata nella tabella correlata con il [proprietà RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) proprietà.  
  
-   Per le colonne di indice, specificare se l'ordinamento è crescente o decrescente con il [proprietà SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) proprietà.  
  
-   Accedere alle proprietà specifiche del provider con il [raccolta di proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
> [!NOTE]
>  Non tutte le proprietà della **colonna** gli oggetti possono essere supportati da provider di dati. Se è stato impostato un valore per una proprietà che non supporta il provider, si verificherà un errore. Per ottenere nuove **colonna** oggetti, l'errore si verifica quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verifica quando l'impostazione della proprietà.  
>   
>  Durante la creazione **colonna** oggetti, l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporta la proprietà. Per altre informazioni sulle proprietà che supporta il provider, vedere la documentazione del provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne aggiungere metodi, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo Connection Close, esempio di proprietà Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di codice: Esempio NumericScale e Precision Properties (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Esempio di proprietà SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
