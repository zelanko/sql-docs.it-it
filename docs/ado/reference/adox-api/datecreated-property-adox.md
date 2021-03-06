---
description: Proprietà DateCreated (ADOX)
title: Proprietà DateCreated (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: rothja
ms.author: jroth
ms.openlocfilehash: 46b94255726bde107e52b6ca9c3546b9744b4a9f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984752"
---
# <a name="datecreated-property-adox"></a>Proprietà DateCreated (ADOX)
Indica la data di creazione dell'oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un valore **Variant** che specifica la data di creazione. Il valore è null se **DateCreated** non è supportato dal provider.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **DateCreated** è null per gli oggetti appena accodati. Dopo aver accodato una nuova [vista](./view-object-adox.md) o [routine](./procedure-object-adox.md), è necessario chiamare il metodo [Refresh](../ado-api/refresh-method-ado.md) della raccolta [views](./views-collection-adox.md) o [Procedures](./procedures-collection-adox.md) per ottenere i valori per la proprietà **DateCreated** .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Procedure (ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto Table (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto View (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà DateCreated e DateModified (VB)](./datecreated-and-datemodified-properties-example-vb.md)   
 [Proprietà DateModified (ADOX)](./datemodified-property-adox.md)