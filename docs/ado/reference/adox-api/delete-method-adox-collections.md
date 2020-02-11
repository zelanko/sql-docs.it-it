---
title: Metodo Delete (raccolte ADOX) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966438"
---
# <a name="delete-method-adox-collections"></a>Metodo Delete (raccolte ADOX)
Rimuove un oggetto da una raccolta.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parametri  
 *Nome*  
 **Variant** che specifica il nome o la posizione ordinale (indice) dell'oggetto da eliminare.  
  
## <a name="remarks"></a>Osservazioni  
 Si verificherà un errore se il *nome* non esiste nella raccolta.  
  
 Per le raccolte di [tabelle](../../../ado/reference/adox-api/tables-collection-adox.md) e [utenti](../../../ado/reference/adox-api/users-collection-adox.md) , si verificherà un errore se il provider non supporta rispettivamente l'eliminazione di tabelle o utenti. Per [le raccolte procedure](../../../ado/reference/adox-api/procedures-collection-adox.md) e [viste](../../../ado/reference/adox-api/views-collection-adox.md) , l' **eliminazione** avrà esito negativo se il provider non supporta la persistenza dei comandi.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Raccolta Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Raccolta di Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Raccolta Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Raccolta Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Raccolta Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Raccolta Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Raccolta Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Raccolta Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Delete delle procedure (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Esempio del metodo Delete di Views (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
