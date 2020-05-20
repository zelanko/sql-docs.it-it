---
title: Oggetto Property (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: rothja
ms.author: jroth
ms.openlocfilehash: d2f4a8b6cdeabcbab0802a0052ed697af70ef45a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759967"
---
# <a name="property-object-ado"></a>Oggetto Property (ADO)
Rappresenta una caratteristica dinamica di un oggetto ADO definito dal provider.  
  
## <a name="remarks"></a>Osservazioni  
 Gli oggetti ADO hanno due tipi di proprietà: incorporata e dinamica.  
  
 Le proprietà predefinite sono quelle implementate in ADO e immediatamente disponibili per qualsiasi nuovo oggetto, usando la `MyObject.Property` sintassi. Non vengono visualizzati come oggetti **Proprietà** nella raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) di un oggetto, quindi, sebbene sia possibile modificarne i valori, non è possibile modificarne le caratteristiche.  
  
 Le proprietà dinamiche sono definite dal provider di dati sottostante e vengono visualizzate nella raccolta **Properties** per l'oggetto ADO appropriato. Una proprietà specifica del provider, ad esempio, può indicare se un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) supporta le transazioni o l'aggiornamento di. Queste proprietà aggiuntive verranno visualizzate come oggetti **Proprietà** nella raccolta delle **proprietà** dell'oggetto **Recordset** . È possibile fare riferimento alle proprietà dinamiche solo tramite la raccolta, usando `MyObject.Properties(0)` la `MyObject.Properties("Name")` sintassi o.  
  
 Non è possibile eliminare entrambi i tipi di proprietà.  
  
 Un oggetto **Proprietà** dinamica dispone di quattro proprietà predefinite:  
  
-   La proprietà [Name](../../../ado/reference/ado-api/name-property-ado.md) è una stringa che identifica la proprietà.  
  
-   La proprietà [Type](../../../ado/reference/ado-api/type-property-ado.md) è un numero intero che specifica il tipo di dati della proprietà.  
  
-   La proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) è una variante che contiene l'impostazione della proprietà. **Value** è la proprietà predefinita per un oggetto **Property** .  
  
-   La proprietà [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) è un valore Long che indica le caratteristiche della proprietà specifica del provider.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Property](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field (oggetto)](../../../ado/reference/ado-api/field-object.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
