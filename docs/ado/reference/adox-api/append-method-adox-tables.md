---
title: Metodo Append (tabelle ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: rothja
ms.author: jroth
ms.openlocfilehash: 19617c65b350527753895ed613f671c3ac0f88e8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764012"
---
# <a name="append-method-adox-tables"></a>Metodo Append (raccolta Tables ADOX)
Aggiunge un nuovo oggetto [Table](../../../ado/reference/adox-api/table-object-adox.md) alla raccolta [Tables](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>Parametri  
 *tavolo*  
 Valore **Variant** che contiene un riferimento alla **tabella** da accodare o il nome della tabella da creare e aggiungere.  
  
## <a name="remarks"></a>Commenti  
 Se il provider non supporta la creazione di tabelle, si verificherà un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Metodo Append (colonne ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Metodo Append (gruppi ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Metodo Append (utenti ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
