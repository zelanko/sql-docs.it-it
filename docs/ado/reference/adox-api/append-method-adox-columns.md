---
description: Metodo Append (raccolta Columns ADOX)
title: Metodo Append (colonne ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c959f6d822724ee6e7480cf00941aaa1fc8012a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985502"
---
# <a name="append-method-adox-columns"></a>Metodo Append (raccolta Columns ADOX)
Aggiunge un nuovo oggetto [Column](./column-object-adox.md) alla raccolta [Columns](./columns-collection-adox.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Colonna*  
 Oggetto **colonna** da aggiungere o nome della colonna da creare e aggiungere.  
  
 *Tipo*  
 Facoltativa. Valore **Long** che specifica il tipo di dati della colonna. Il parametro di *tipo* corrisponde alla proprietà [Type](./type-property-column-adox.md) di un oggetto **Column** .  
  
 *DefinedSize*  
 Facoltativa. Valore **Long** che specifica le dimensioni della colonna. Il parametro *DefinedSize* corrisponde alla proprietà [DefinedSize](./definedsize-property-adox.md) di un oggetto **Column** .  
  
> [!NOTE]
>  Si verificherà un errore durante l'aggiunta di una **colonna** alla raccolta **Columns** di un [Indice](./index-object-adox.md) se la **colonna** non esiste in una [tabella](./table-object-adox.md) già accodata alla raccolta [Tables](./tables-collection-adox.md) .  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta Columns (ADOX)](./columns-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Accodamento di colonne e tabelle, esempio di proprietà Name (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Esempio di proprietà Method Append, Key Type, RelatedColumn, RelatedTable e UpdateRule (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Metodo Append (gruppi ADOX)](./append-method-adox-groups.md)   
 [Metodo Append (indici ADOX)](./append-method-adox-indexes.md)   
 [Metodo Append (chiavi ADOX)](./append-method-adox-keys.md)   
 [Metodo Append (routine ADOX)](./append-method-adox-procedures.md)   
 [Metodo Append (tabelle ADOX)](./append-method-adox-tables.md)   
 [Metodo Append (utenti ADOX)](./append-method-adox-users.md)   
 [Metodo Append (raccolta Views ADOX)](./append-method-adox-views.md)