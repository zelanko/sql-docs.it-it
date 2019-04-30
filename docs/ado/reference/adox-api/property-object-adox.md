---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2502dcdab170102f526aa1ea0fe67235e6bf3048
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281904"
---
# <a name="property-object-adox"></a>Oggetto Property (ADOX)
Rappresenta una caratteristica di un oggetto ADOX.  
  
## <a name="remarks"></a>Note  
 Oggetti ADOX hanno due tipi di proprietà: predefinito e dinamico.  
  
 Proprietà predefinite sono immediatamente disponibili per qualsiasi nuovo oggetto, utilizzando la sintassi MyObject tali proprietà. Non sono visualizzate come oggetti di proprietà in un oggetto [raccolta di proprietà](../../../ado/reference/ado-api/properties-collection-ado.md), pertanto anche se è possibile modificarne i valori, è possibile modificare le relative caratteristiche.  
  
 Proprietà dinamiche sono definite dal provider di dati sottostanti e vengono visualizzati nella raccolta delle proprietà per l'oggetto ADOX appropriato.  Proprietà dinamiche è possibile fare riferimento solo tramite la raccolta, usando la sintassi MyObject.Properties(0) o MyObject.  
  
 Non è possibile eliminare entrambi i tipi di proprietà.  
  
 Un oggetto dinamico di proprietà presenta quattro proprietà incorporate propri:  
  
 Il [nome](../../../ado/reference/ado-api/name-property-ado.md) proprietà è una stringa che identifica la proprietà.  
  
 Il [tipo](../../../ado/reference/ado-api/type-property-ado.md) proprietà è un numero intero che specifica il tipo di dati di proprietà.  
  
 Il [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà è una variante che contiene l'impostazione della proprietà. Valore è la proprietà predefinita per un oggetto proprietà.  
  
 Il [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà è un valore long che indica le caratteristiche della proprietà specifiche del provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto Property ADOX](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
