---
title: Metodo Append (chiavi ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd66edb75bec4f4b7e35c53c9ebeabd9b3c75d83
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967295"
---
# <a name="append-method-adox-keys"></a>Metodo Append (raccolta Keys ADOX)
Aggiunge un nuovo oggetto [chiave](../../../ado/reference/adox-api/key-object-adox.md) alla raccolta di [chiavi](../../../ado/reference/adox-api/keys-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Codice*  
 Oggetto **chiave** da accodare o nome della chiave da creare e aggiungere.  
  
 *KeyType*  
 Facoltativa. Valore **Long** che specifica il tipo di chiave. Il parametro *Key* corrisponde alla proprietà [Type](../../../ado/reference/adox-api/type-property-key-adox.md) di un oggetto **Key** .  
  
 *Colonna*  
 Facoltativa. Valore **stringa** che specifica il nome della colonna da indicizzare. Il parametro *Columns* corrisponde al valore della proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) di un oggetto [Column](../../../ado/reference/adox-api/column-object-adox.md) .  
  
 *RelatedTable*  
 Facoltativa. Valore **stringa** che specifica il nome della tabella correlata. Il parametro *RelatedTable* corrisponde al valore della proprietà **Name** di un oggetto [Table](../../../ado/reference/adox-api/table-object-adox.md) .  
  
 *RelatedColumn*  
 Facoltativa. Valore **stringa** che specifica il nome della colonna correlata per una chiave esterna. Il parametro *RelatedColumn* corrisponde al valore della proprietà **Name** di un oggetto [Column](../../../ado/reference/adox-api/column-object-adox.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Il parametro *Columns* può assumere il nome di una colonna o una matrice di nomi di colonna.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
