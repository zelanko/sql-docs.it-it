---
title: Oggetto Catalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9843ad9ac0a456f7e38e741e08ce9b66f862fd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967051"
---
# <a name="catalog-object-adox"></a>Oggetto Catalog (ADOX)
Contiene le raccolte ([tabelle](../../../ado/reference/adox-api/tables-collection-adox.md), [viste](../../../ado/reference/adox-api/views-collection-adox.md), [utenti](../../../ado/reference/adox-api/users-collection-adox.md), [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md)e [procedure](../../../ado/reference/adox-api/procedures-collection-adox.md)) che descrivono il catalogo dello schema di un'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile modificare l'oggetto **Catalogo** aggiungendo o rimuovendo oggetti o modificando gli oggetti esistenti. Alcuni provider potrebbero non supportare tutti gli oggetti del **Catalogo** o supportare solo la visualizzazione delle informazioni sullo schema.  
  
 Con le proprietà e i metodi di un oggetto **Catalogo** , è possibile:  
  
-   Aprire il catalogo impostando la proprietà [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) su un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) ADO o una stringa di connessione valida.  
  
-   Creare un nuovo catalogo con il metodo [create](../../../ado/reference/adox-api/create-method-adox.md) .  
  
-   Determinare i proprietari degli oggetti in un **Catalogo** con i metodi [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Catalog](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection di Catalog (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Esempio di proprietà Command e CommandText (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Metodo di chiusura della connessione, esempio di proprietà del tipo di tabella (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Esempio di metodo Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Raccolta Parameters, esempio di proprietà Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Esempio di metodo Append di procedure (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Esempio di metodo Delete delle procedure (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Esempio di metodo Refresh di Procedures (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Esempio di raccolte views e Fields (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Esempio di metodo Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Raccolta views, esempio di proprietà CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Esempio di metodo Delete views (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Esempio di metodo Refresh views (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Raccolta Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Raccolta Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Raccolta utenti (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Raccolta Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
