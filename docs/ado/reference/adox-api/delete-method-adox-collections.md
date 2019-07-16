---
title: Metodo (raccolte ADOX) Delete | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be2aa91cf27d7dc12d3cd0c1e0bf719bd43797ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966438"
---
# <a name="delete-method-adox-collections"></a>Metodo Delete (raccolte ADOX)
Rimuove un oggetto da una raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parametri  
 *Name*  
 Oggetto **Variant** che specifica il nome o la posizione (indice) dell'oggetto da eliminare.  
  
## <a name="remarks"></a>Note  
 Si verifica un errore se il *nome* non esiste nella raccolta.  
  
 Per la [tabelle](../../../ado/reference/adox-api/tables-collection-adox.md) e [utenti](../../../ado/reference/adox-api/users-collection-adox.md) raccolte, viene visualizzato un errore se il provider non supporta l'eliminazione di tabelle o gli utenti, rispettivamente. Per [procedure](../../../ado/reference/adox-api/procedures-collection-adox.md) e [viste](../../../ado/reference/adox-api/views-collection-adox.md) raccolte **Elimina** avrà esito negativo se il provider non supporta comandi di persistenza.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta di oggetti Column (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta di oggetti Group (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta di oggetti Index (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta di oggetti Key (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta di oggetti Procedure (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Raccolta di oggetti Table (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Raccolta di oggetti User (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Raccolta di oggetti View (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure di esempio del metodo Delete (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Esempio di metodo Delete oggetti View (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
