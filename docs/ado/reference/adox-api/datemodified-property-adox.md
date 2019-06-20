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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5d0cd8a6196bdc0f933470a52dbb3567f64df05e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718914"
---
# <a name="datemodified-property-adox"></a>Proprietà DateModified (ADOX)
Indica la data che dell'ultima modifica dell'oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
 Restituisce un **Variant** valore che specifica la data di modifica. Il valore è null se **DateModified** non è supportato dal provider.  
  
## <a name="remarks"></a>Note  
 Il **DateModified** proprietà è null per gli oggetti appena aggiunti. Dopo aver aggiunto un nuovo [vista](../../../ado/reference/adox-api/view-object-adox.md) o [Procedure](../../../ado/reference/adox-api/procedure-object-adox.md), è necessario chiamare il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) metodo il [viste](../../../ado/reference/adox-api/views-collection-adox.md) o [procedure ](../../../ado/reference/adox-api/procedures-collection-adox.md) insieme per ottenere valori per il **DateModified** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Oggetto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Oggetto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà DateCreated e DateModified (esempio di proprietà (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [Proprietà DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
