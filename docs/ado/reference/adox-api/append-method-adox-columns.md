---
title: Metodo Append (colonne ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6493157c00e5a71c7c2f085191231bb33bb5279a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967321"
---
# <a name="append-method-adox-columns"></a>Metodo Append (raccolta Columns ADOX)
Aggiunge un nuovo oggetto [Column](../../../ado/reference/adox-api/column-object-adox.md) alla raccolta [Columns](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Colonna*  
 Oggetto **colonna** da aggiungere o nome della colonna da creare e aggiungere.  
  
 *Tipo*  
 Facoltativa. Valore **Long** che specifica il tipo di dati della colonna. Il parametro di *tipo* corrisponde alla proprietà [Type](../../../ado/reference/adox-api/type-property-column-adox.md) di un oggetto **Column** .  
  
 *DefinedSize*  
 Facoltativa. Valore **Long** che specifica le dimensioni della colonna. Il parametro *DefinedSize* corrisponde alla proprietà [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) di un oggetto **Column** .  
  
> [!NOTE]
>  Si verificherà un errore durante l'aggiunta di una **colonna** alla raccolta **Columns** di un [Indice](../../../ado/reference/adox-api/index-object-adox.md) se la **colonna** non esiste in una [tabella](../../../ado/reference/adox-api/table-object-adox.md) già accodata alla raccolta [Tables](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (raccolta Views ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
