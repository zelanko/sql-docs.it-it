---
description: Oggetto Key (ADOX)
title: Oggetto Key (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 619cd72854a4e779fbea8989fa84ef6fdf27f90a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770110"
---
# <a name="key-object-adox"></a>Oggetto Key (ADOX)
Rappresenta un campo chiave primaria, esterna o univoca di una tabella di database.  
  
## <a name="remarks"></a>Commenti  
 Il codice seguente crea una nuova **chiave**:  
  
```  
Dim obj As New Key  
```  
  
 Con le proprietà e le raccolte di un oggetto **chiave** , è possibile:  
  
-   Identificare la chiave con la proprietà [Name](./name-property-adox.md) .  
  
-   Determinare se la chiave è primaria, esterna o univoca con la proprietà [Type](./type-property-key-adox.md) .  
  
-   Accedere alle colonne di database della chiave con la raccolta [Columns](./columns-collection-adox.md) .  
  
-   Specificare il nome della tabella correlata con la proprietà [RelatedTable](./relatedtable-property-adox.md) .  
  
-   Determinare l'azione eseguita per l'eliminazione o l'aggiornamento di una chiave primaria con le proprietà [DeleteRule](./deleterule-property-adox.md) e [UpdateRule](./updaterule-property-adox.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Key](./key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Raccolta Columns (ADOX)](./columns-collection-adox.md)   
 [Raccolta Keys (ADOX)](./keys-collection-adox.md)