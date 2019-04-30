---
title: Append (metodo) (oggetti Index ADOX) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 18e9162c3c9a1b79c28ca6e0ae94f8680db0ac80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206265"
---
# <a name="append-method-adox-indexes"></a>Metodo Append (raccolta Indexes ADOX)
Aggiunge un nuovo [indice](../../../ado/reference/adox-api/index-object-adox.md) dell'oggetto per il [indici](../../../ado/reference/adox-api/indexes-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Index*  
 Il **indice** il nome dell'indice per creare e aggiungere o oggetto da accodare.  
  
 *Colonne*  
 Facoltativo. Oggetto **Variant** valore che specifica i nomi delle colonne da indicizzare. Il *colonne* parametro corrisponde ai valori della [Name](../../../ado/reference/adox-api/name-property-adox.md) proprietà di un [colonna](../../../ado/reference/adox-api/column-object-adox.md) o più oggetti.  
  
## <a name="remarks"></a>Note  
 Il *colonne* parametro può accettare il nome di una colonna o una matrice di nomi di colonna.  
  
 Se il provider non supporta la creazione di indici, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Index (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo (VB) Append](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append (metodo) (oggetti Column ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (metodo) (oggetti Group ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti procedure ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (metodo) (User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
