---
title: Assegnare un nome proprietà (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52808cf9e90c6779efb9f95e385f8df501bae870
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965751"
---
# <a name="name-property-adox"></a>Proprietà Name (ADOX)
Indica il nome dell'oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore.  
  
## <a name="remarks"></a>Note  
 I nomi non sono necessario essere univoco all'interno di una raccolta.  
  
 Il **Name** è di lettura/scrittura in [colonna](../../../ado/reference/adox-api/column-object-adox.md), [gruppo](../../../ado/reference/adox-api/group-object-adox.md), [chiave](../../../ado/reference/adox-api/key-object-adox.md), [indice](../../../ado/reference/adox-api/index-object-adox.md), [ Nella tabella](../../../ado/reference/adox-api/table-object-adox.md), e [utente](../../../ado/reference/adox-api/user-object-adox.md) oggetti. Il **Name** proprietà è di sola lettura nel [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md), [Procedure](../../../ado/reference/adox-api/procedure-object-adox.md), e [vista](../../../ado/reference/adox-api/view-object-adox.md) oggetti.  
  
 Per gli oggetti di lettura/scrittura (**colonna**, **gruppo**, **chiave**, **indice**, **tabella** e  **Utente** oggetti), il valore predefinito è una stringa vuota ("").  
  
> [!NOTE]
>  Per le chiavi, questa proprietà è di sola lettura sul **chiave** già aggiunti a una raccolta di oggetti. Per le tabelle, questa proprietà è di sola lettura per **tabella** già aggiunti a una raccolta di oggetti.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Oggetto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Oggetto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Oggetto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Oggetto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Oggetto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne aggiungere metodi, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
