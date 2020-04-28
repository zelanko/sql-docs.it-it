---
title: Oggetto Table (ADOX) | Microsoft Docs
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
ms.openlocfilehash: 10f3add3cb243d54643c3294104ec2546e7737d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965161"
---
# <a name="table-object-adox"></a>Oggetto Table (ADOX)
Rappresenta una tabella di database che include colonne, indici e chiavi.  
  
## <a name="remarks"></a>Osservazioni  
 Il codice seguente crea una nuova **tabella**:  
  
```  
Dim obj As New Table  
```  
  
 Con le proprietà e le raccolte di un oggetto **Table** è possibile:  
  
-   Identificare la tabella con la proprietà [Name Property (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determinare il tipo di tabella con la proprietà del [tipo (tabella) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) .  
  
-   Accedere alle colonne di database della tabella con la raccolta [Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Accedere agli indici della tabella con la [raccolta Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Accedere alle chiavi della tabella con la [raccolta Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Specificare il catalogo proprietario della tabella con la proprietà [ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) .  
  
-   Restituire le informazioni sulla data con le proprietà [DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DATEMODIFIED Property (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) .  
  
-   Accedere alle proprietà di tabella specifiche del provider con la raccolta [Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Il provider di dati potrebbe non supportare tutte le proprietà degli oggetti **tabella** . Se è stato impostato un valore per una proprietà non supportata dal provider, si verificherà un errore. Per i nuovi oggetti **tabella** , l'errore si verificherà quando l'oggetto viene aggiunto alla raccolta. Per gli oggetti esistenti, l'errore si verificherà quando si imposta la proprietà.  
>   
>  Quando si creano oggetti **tabella** , l'esistenza di un valore predefinito appropriato per una proprietà facoltativa non garantisce che il provider supporti la proprietà. Per ulteriori informazioni sulle proprietà supportate dal provider, vedere la documentazione del provider.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection di Catalog (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo di chiusura della connessione, esempio di proprietà del tipo di tabella (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Raccolta Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
