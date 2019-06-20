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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: af077c1606148eacb4f93ba6cfb52c3bb5eeefce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702950"
---
# <a name="property-object-ado"></a>Oggetto Property (ADO)
Rappresenta una caratteristica dinamica di un oggetto ADO che viene definito dal provider.  
  
## <a name="remarks"></a>Note  
 Gli oggetti ADO presentano due tipi di proprietà: predefinito e dinamico.  
  
 Proprietà predefinite sono le proprietà implementate in ADO e immediatamente disponibili per qualsiasi nuovo oggetto, tramite il `MyObject.Property` sintassi. Non sono visualizzate come **proprietà** gli oggetti in un oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme, in modo che anche se è possibile modificarne i valori, è possibile modificare le relative caratteristiche.  
  
 Proprietà dinamiche sono definite dal provider di dati sottostanti e vengono visualizzati nei **proprietà** raccolta per l'oggetto ADO appropriato. Ad esempio, una proprietà specifica del provider può indicare se un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto supporta le transazioni o l'aggiornamento. Queste proprietà aggiuntive verranno visualizzato come **proprietà** gli oggetti in quanto **Recordset** dell'oggetto **proprietà** raccolta. Proprietà dinamiche è possibile fare riferimento solo all'interno dell'insieme, utilizzando il `MyObject.Properties(0)` o `MyObject.Properties("Name")` sintassi.  
  
 Non è possibile eliminare entrambi i tipi di proprietà.  
  
 Dinamico **proprietà** oggetto dispone di quattro proprietà incorporate propri:  
  
-   Il [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà è una stringa che identifica la proprietà.  
  
-   Il [tipo](../../../ado/reference/ado-api/type-property-ado.md) proprietà è un numero intero che specifica il tipo di dati di proprietà.  
  
-   Il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà è una variante che contiene l'impostazione della proprietà. **Valore** è la proprietà predefinita per un **proprietà** oggetto.  
  
-   Il [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà è un valore long che indica le caratteristiche della proprietà specifiche del provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà dell'oggetto proprietà, metodi ed eventi](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
