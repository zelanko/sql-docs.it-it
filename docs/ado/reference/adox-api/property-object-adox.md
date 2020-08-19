---
description: Oggetto Property (ADOX)
title: Oggetto Property (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a836b5b0778aea77732036d1951db81aa790198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439603"
---
# <a name="property-object-adox"></a>Oggetto Property (ADOX)
Rappresenta una caratteristica di un oggetto ADOX.  
  
## <a name="remarks"></a>Osservazioni  
 Gli oggetti ADOX hanno due tipi di proprietà: incorporata e dinamica.  
  
 Le proprietà predefinite sono tali proprietà immediatamente disponibili per qualsiasi nuovo oggetto, utilizzando la sintassi myObject. Property. Non vengono visualizzati come oggetti proprietà nella [raccolta delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md)di un oggetto, quindi, sebbene sia possibile modificarne i valori, non è possibile modificarne le caratteristiche.  
  
 Le proprietà dinamiche sono definite dal provider di dati sottostante e vengono visualizzate nella raccolta Properties per l'oggetto ADOX appropriato.  È possibile fare riferimento alle proprietà dinamiche solo tramite la raccolta, usando la sintassi oggetti. Properties (0) o MyObject. Properties ("Name").  
  
 Non è possibile eliminare entrambi i tipi di proprietà.  
  
 Un oggetto proprietà dinamica dispone di quattro proprietà predefinite:  
  
 La proprietà [Name](../../../ado/reference/ado-api/name-property-ado.md) è una stringa che identifica la proprietà.  
  
 La proprietà [Type](../../../ado/reference/ado-api/type-property-ado.md) è un numero intero che specifica il tipo di dati della proprietà.  
  
 La proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) è una variante che contiene l'impostazione della proprietà. Value è la proprietà predefinita per un oggetto Property.  
  
 La proprietà [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) è un valore Long che indica le caratteristiche della proprietà specifica del provider.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Property ADOX](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
