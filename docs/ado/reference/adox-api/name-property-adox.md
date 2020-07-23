---
title: Proprietà Name (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 24d86b384a1eb2916e488c17c99e4b9b5962dd1a
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942723"
---
# <a name="name-property-adox"></a>Proprietà Name (ADOX)
Indica il nome dell'oggetto.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** .  
  
## <a name="remarks"></a>Osservazioni  
 Non è necessario che i nomi siano univoci all'interno di una raccolta.  
  
 La proprietà **Name** è di lettura/scrittura negli oggetti [Column](../../../ado/reference/adox-api/column-object-adox.md), [Group](../../../ado/reference/adox-api/group-object-adox.md), [Key](../../../ado/reference/adox-api/key-object-adox.md), [index](../../../ado/reference/adox-api/index-object-adox.md), [Table](../../../ado/reference/adox-api/table-object-adox.md)e [User](../../../ado/reference/adox-api/user-object-adox.md) . La proprietà **Name** è di sola lettura negli oggetti [Catalog](../../../ado/reference/adox-api/catalog-object-adox.md), [procedure](../../../ado/reference/adox-api/procedure-object-adox.md)e [visualizzazione](../../../ado/reference/adox-api/view-object-adox.md) .  
  
 Per gli oggetti di lettura/scrittura (**colonna**, **gruppo**, **chiave**, **Indice**, **tabella** e oggetti **utente** ), il valore predefinito è una stringa vuota ("").  
  
> [!NOTE]
>  Per le chiavi, questa proprietà è di sola lettura sugli oggetti **chiave** già accodati a una raccolta. Per le tabelle, questa proprietà è di sola lettura per gli oggetti **tabella** già accodati a una raccolta.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
        [Oggetto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
        [Oggetto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)  
        [Oggetto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
        [Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
        [Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
        [Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
