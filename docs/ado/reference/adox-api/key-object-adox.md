---
title: Chiave oggetto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6dbbb81d53755032725ad71ff9bbf49b9beb2f1c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706480"
---
# <a name="key-object-adox"></a>Oggetto Key (ADOX)
Rappresenta un campo di chiave primario, esterno o univoco da una tabella di database.  
  
## <a name="remarks"></a>Note  
 Il codice seguente crea una nuova **chiave**:  
  
```  
Dim obj As New Key  
```  
  
 Con le proprietà e raccolte di un **chiave** dell'oggetto, è possibile:  
  
-   Identificare la chiave con il [nome](../../../ado/reference/adox-api/name-property-adox.md) proprietà.  
  
-   Determinare se la chiave è primaria, esterna o univoco con il [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) proprietà.  
  
-   Accedere alle colonne del database della chiave con il [colonne](../../../ado/reference/adox-api/columns-collection-adox.md) raccolta.  
  
-   Specificare il nome della tabella correlata con il [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) proprietà.  
  
-   Determinare l'azione eseguita su eliminazione o aggiornamento di una chiave primaria con la [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) e [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) proprietà.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Raccolta di colonne (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
