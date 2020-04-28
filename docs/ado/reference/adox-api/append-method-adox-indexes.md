---
title: Metodo Append (indici ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef30faf0fef05c4e86ffb4d2c21781592094c198
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967309"
---
# <a name="append-method-adox-indexes"></a>Metodo Append (raccolta Indexes ADOX)
Aggiunge un nuovo oggetto [index](../../../ado/reference/adox-api/index-object-adox.md) alla raccolta [indexes](../../../ado/reference/adox-api/indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Indice*  
 Oggetto **index** da accodare o il nome dell'indice da creare e accodare.  
  
 *Colonne*  
 Facoltativa. Valore **Variant** che specifica il nome o i nomi delle colonne da indicizzare. Il parametro *Columns* corrisponde ai valori della proprietà [Name](../../../ado/reference/adox-api/name-property-adox.md) di un oggetto [colonna](../../../ado/reference/adox-api/column-object-adox.md) o di oggetti.  
  
## <a name="remarks"></a>Osservazioni  
 Il parametro *Columns* può assumere il nome di una colonna o una matrice di nomi di colonna.  
  
 Se il provider non supporta la creazione di indici, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Index (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Append degli indici (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
