---
title: Proprietà DateModified (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: rothja
ms.author: jroth
ms.openlocfilehash: ccd916a8b9e9c500d3b718371b01831cc0ef292f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759207"
---
# <a name="datemodified-property-adox"></a>Proprietà DateModified (ADOX)
Indica la data dell'Ultima modifica apportata all'oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Variant** che specifica la data di modifica. Il valore è null se **DateModified** non è supportato dal provider.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **DateModified** è null per gli oggetti appena accodati. Dopo aver accodato una nuova [vista](../../../ado/reference/adox-api/view-object-adox.md) o [routine](../../../ado/reference/adox-api/procedure-object-adox.md), è necessario chiamare il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) della raccolta [views](../../../ado/reference/adox-api/views-collection-adox.md) o [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) per ottenere i valori per la proprietà **DateModified** .  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà DateCreated e DateModified (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [Proprietà DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
