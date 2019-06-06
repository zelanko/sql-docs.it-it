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
manager: jroth
ms.openlocfilehash: 7cdadbf3db6447f46fefac19d4979c266165905f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708072"
---
# <a name="catalog-object-adox"></a>Oggetto Catalog (ADOX)
Contiene raccolte ([tabelle](../../../ado/reference/adox-api/tables-collection-adox.md), [viste](../../../ado/reference/adox-api/views-collection-adox.md), [utenti](../../../ado/reference/adox-api/users-collection-adox.md), [gruppi](../../../ado/reference/adox-api/groups-collection-adox.md), e [procedure](../../../ado/reference/adox-api/procedures-collection-adox.md)) che viene descritto il catalogo dello schema di un'origine dati.  
  
## <a name="remarks"></a>Note  
 È possibile modificare il **catalogo** oggetto aggiungendo o rimuovendo gli oggetti o modificando gli oggetti esistenti. Alcuni provider potrebbero non supportare tutte le **catalogo** oggetti o può supportare solo la visualizzazione delle informazioni sullo schema.  
  
 Con le proprietà e metodi di una **catalogo** dell'oggetto, è possibile:  
  
-   Aprire il catalogo impostando il [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) proprietà di un oggetto ADO [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto o una stringa di connessione valida.  
  
-   Crea un nuovo catalogo con il [Create](../../../ado/reference/adox-api/create-method-adox.md) (metodo).  
  
-   Determinare i proprietari degli oggetti in un **Catalog** con il [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner (ADOX)](../../../ado/reference/adox-api/setobjectowner-method.md) metodi.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Catalog](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection di Catalog (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Esempio di proprietà CommandText (VB) e comandi](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Metodo Connection Close, esempio di proprietà Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Esempio del metodo Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Raccolta di parametri, esempio di proprietà Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Procedure di esempio del metodo Append (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Procedure di esempio del metodo Delete (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Procedure di esempio del metodo Refresh (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Viste e esempio di raccolte di campi (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Viste di esempio del metodo Append (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Raccolta di oggetti View, esempio di proprietà CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Viste di esempio del metodo Delete (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Viste di esempio del metodo Refresh (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Raccolta di gruppi (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Raccolta di oggetti procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Raccolta di tabelle (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Raccolta degli utenti (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
