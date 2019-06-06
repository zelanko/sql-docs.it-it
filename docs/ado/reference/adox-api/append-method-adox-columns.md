---
title: Append (metodo) (oggetti Column ADOX) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: e8ac03231680ecd807234b20ac7b210bc480f2c1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708489"
---
# <a name="append-method-adox-columns"></a>Metodo Append (raccolta Columns ADOX)
Aggiunge un nuovo [colonna](../../../ado/reference/adox-api/column-object-adox.md) dell'oggetto per il [colonne](../../../ado/reference/adox-api/columns-collection-adox.md) raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parametri  
 *Colonna*  
 Il **colonna** il nome della colonna per creare e aggiungere o oggetto da accodare.  
  
 *Tipo*  
 Facoltativo. Oggetto **lungo** valore che specifica il tipo di dati della colonna. Il *tipo* parametro corrisponde per il [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) proprietà di un **colonna** oggetto.  
  
 *DefinedSize*  
 Facoltativo. Oggetto **lungo** valore che specifica la dimensione della colonna. Il *DefinedSize* parametro corrisponde per il [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) proprietà di un **colonna** oggetto.  
  
> [!NOTE]
>  Si verifica un errore quando si aggiunge un **colonna** per il **colonne** raccolta di un [indice](../../../ado/reference/adox-api/index-object-adox.md) se il **colonna** non esiste in un [Nella tabella](../../../ado/reference/adox-api/table-object-adox.md) già aggiunto al [tabelle](../../../ado/reference/adox-api/tables-collection-adox.md) raccolta.  
  
## <a name="applies-to"></a>Si applica a  
 [Raccolta di oggetti Column (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne aggiungere metodi, esempio di proprietà Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Append oggetti Key (metodo), tipo di chiave, RelatedColumn, RelatedTable e UpdateRule (esempio di proprietà (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append (metodo) (oggetti Group ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (metodo) (oggetti Index ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (metodo) (oggetti Key ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (metodo) (oggetti procedure ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (metodo) (oggetti Table ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (metodo) (User ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Metodo Append (oggetti View ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
