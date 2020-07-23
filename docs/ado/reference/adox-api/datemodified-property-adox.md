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
ms.openlocfilehash: 1c3a2a8ba0890dd50621fac143aa102091abcc19
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942713"
---
# <a name="datemodified-property-adox"></a>Proprietà DateModified (ADOX)
Indica la data dell'Ultima modifica apportata all'oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Variant** che specifica la data di modifica. Il valore è null se **DateModified** non è supportato dal provider.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **DateModified** è null per gli oggetti appena accodati. Dopo aver accodato una nuova [vista](../../../ado/reference/adox-api/view-object-adox.md) o [routine](../../../ado/reference/adox-api/procedure-object-adox.md), è necessario chiamare il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) della raccolta [views](../../../ado/reference/adox-api/views-collection-adox.md) o [Procedures](../../../ado/reference/adox-api/procedures-collection-adox.md) per ottenere i valori per la proprietà **DateModified** .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà DateCreated e DateModified (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [Proprietà DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
