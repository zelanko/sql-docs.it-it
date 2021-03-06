---
description: Metodo Append (raccolta Keys ADOX)
title: Metodo Append (chiavi ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2531031808c16db4892fb0b759a8a8d819a2222d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985482"
---
# <a name="append-method-adox-keys"></a>Metodo Append (raccolta Keys ADOX)
Aggiunge un nuovo oggetto [chiave](./key-object-adox.md) alla raccolta di [chiavi](./keys-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Chiave*  
 Oggetto **chiave** da accodare o nome della chiave da creare e aggiungere.  
  
 *KeyType*  
 Facoltativa. Valore **Long** che specifica il tipo di chiave. Il parametro *Key* corrisponde alla proprietà [Type](./type-property-key-adox.md) di un oggetto **Key** .  
  
 *Colonna*  
 Facoltativa. Valore **stringa** che specifica il nome della colonna da indicizzare. Il parametro *Columns* corrisponde al valore della proprietà [Name](./name-property-adox.md) di un oggetto [Column](./column-object-adox.md) .  
  
 *RelatedTable*  
 Facoltativa. Valore **stringa** che specifica il nome della tabella correlata. Il parametro *RelatedTable* corrisponde al valore della proprietà **Name** di un oggetto [Table](./table-object-adox.md) .  
  
 *RelatedColumn*  
 Facoltativa. Valore **stringa** che specifica il nome della colonna correlata per una chiave esterna. Il parametro *RelatedColumn* corrisponde al valore della proprietà **Name** di un oggetto [Column](./column-object-adox.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Il parametro *Columns* può assumere il nome di una colonna o una matrice di nomi di colonna.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Keys (ADOX)](./keys-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Metodo Append (colonne ADOX)](./append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](./append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](./append-method-adox-indexes.md)   
 [Metodo Append (routine ADOX)](./append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](./append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](./append-method-adox-users.md)   
 [Metodo Append (raccolta Views ADOX)](./append-method-adox-views.md)