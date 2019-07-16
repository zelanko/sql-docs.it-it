---
title: Tabelle insieme (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bf28af10084a30a5c81c76fe7e44781178979ad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965136"
---
# <a name="tables-collection-adox"></a>Raccolta Tables (ADOX)
Contiene tutti [tabella](../../../ado/reference/adox-api/table-object-adox.md) gli oggetti di un catalogo.  
  
## <a name="remarks"></a>Note  
 Il [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) metodo per un **tabelle** raccolta sia univoca per ADOX. È possibile:  
  
-   Aggiungere una nuova tabella alla raccolta con il **Append** (metodo).  
  
 Le proprietà e metodi restanti sono standard per le raccolte di ADO. È possibile:  
  
-   Accedere a una tabella nella raccolta con il [elemento](../../../ado/reference/ado-api/item-property-ado.md) proprietà.  
  
-   Restituisce il numero di tabelle contenute nella raccolta con il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà.  
  
-   Rimuovere una tabella dalla raccolta con il [eliminare](../../../ado/reference/adox-api/delete-method-adox-collections.md) (metodo).  
  
-   Aggiornare gli oggetti nella raccolta in modo da riflettere lo schema del database corrente con il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) (metodo).  
  
 Alcuni provider può restituire altri oggetti dello schema, ad esempio una vista, nel **tabelle** raccolta. Di conseguenza, alcune raccolte ADOX possono contenere più riferimenti allo stesso oggetto. È necessario eliminare l'oggetto da una raccolta, la modifica non saranno visibile in un'altra raccolta che fa riferimento all'oggetto eliminato finché il **Aggiorna** metodo viene chiamato nell'insieme. Ad esempio, con il Provider OLE DB per Microsoft Jet, le visualizzazioni vengono restituite con la **tabelle** raccolta. Se si elimina una vista, è necessario aggiornare il **tabelle** raccolta prima che la raccolta rifletteranno le modifiche.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi della raccolta di oggetti Table](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection di Catalog (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Tabelle e colonne aggiungere metodi, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Metodo Connection Close, esempio di proprietà Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Oggetto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
