---
title: Proprietà ParentCatalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c146e53379f1a81948135d9d993150f4e1e4046e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706346"
---
# <a name="parentcatalog-property-adox"></a>Proprietà ParentCatalog (ADOX)
Specifica il catalogo padre di un oggetto tabella, un utente o colonna per fornire l'accesso a proprietà specifiche del provider.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta e restituisce un [catalogo](../../../ado/reference/adox-api/catalog-object-adox.md) oggetto. L'impostazione **ParentCatalog** a un elemento aperto **catalogo** consente l'accesso a proprietà specifiche del provider prima di aggiungere una tabella o colonna di una **catalogo** raccolta.  
  
## <a name="remarks"></a>Note  
 Alcuni provider di dati i valori delle proprietà specifiche del provider deve essere scritto solo al momento della creazione: vale a dire, quando una tabella o colonna viene aggiunto al relativo **catalogo** raccolta. Accedere a queste proprietà prima di aggiungere questi oggetti a un **Catalog**, specificare il **catalogo** nel **ParentCatalog** proprietà prima.  
  
 Si verifica un errore quando la tabella o la colonna viene aggiunta a un diverso **Catalog** rispetto al **ParentCatalog**.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Oggetto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
