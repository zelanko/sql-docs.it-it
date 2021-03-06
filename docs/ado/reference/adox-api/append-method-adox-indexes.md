---
description: Metodo Append (raccolta Indexes ADOX)
title: Metodo Append (indici ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b37055efe15f204049d02c337b54c228468419
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985512"
---
# <a name="append-method-adox-indexes"></a>Metodo Append (raccolta Indexes ADOX)
Aggiunge un nuovo oggetto [index](./index-object-adox.md) alla raccolta [indexes](./indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Index*  
 Oggetto **index** da accodare o il nome dell'indice da creare e accodare.  
  
 *Colonne*  
 Facoltativa. Valore **Variant** che specifica il nome o i nomi delle colonne da indicizzare. Il parametro *Columns* corrisponde ai valori della proprietà [Name](./name-property-adox.md) di un oggetto [colonna](./column-object-adox.md) o di oggetti.  
  
## <a name="remarks"></a>Osservazioni  
 Il parametro *Columns* può assumere il nome di una colonna o una matrice di nomi di colonna.  
  
 Se il provider non supporta la creazione di indici, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Indexes (ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append degli indici (VB)](./indexes-append-method-example-vb.md)   
 [Metodo Append (colonne ADOX)](./append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](./append-method-adox-groups.md)   
 [Metodo Append (chiavi ADOX)](./append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](./append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](./append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](./append-method-adox-users.md)   
 [Metodo Append (raccolta Views ADOX)](./append-method-adox-views.md)