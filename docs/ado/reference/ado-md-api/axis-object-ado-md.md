---
description: Oggetto Axis (ADO MD)
title: Oggetto Axis (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: f280021ec705bf530b77bce695510eccd654ce88
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778370"
---
# <a name="axis-object-ado-md"></a>Oggetto Axis (ADO MD)
Rappresenta un asse posizionale o di filtro di un oggetto Cell, contenente i membri selezionati di una o più dimensioni.  
  
## <a name="remarks"></a>Commenti  
 Un oggetto **Axis** può essere contenuto da una raccolta di [assi](./axes-collection-ado-md.md) o restituito dalla proprietà [FilterAxis](./filteraxis-property-ado-md.md) di un oggetto [Cell](./cellset-object-ado-md.md).  
  
 Con le raccolte e le proprietà di un oggetto **asse** , è possibile eseguire le operazioni seguenti:  
  
-   Identificare l' **asse** con la proprietà [Name](./name-property-ado-md.md) .  
  
-   Scorrere ogni posizione lungo un **asse** utilizzando la raccolta [Positions](./positions-collection-ado-md.md) .  
  
-   Ottenere il numero di dimensioni sull' **asse** con la proprietà [DimensionCount](./dimensioncount-property-ado-md.md) .  
  
-   Ottenere gli attributi specifici del provider dell' **asse** con la raccolta delle [Proprietà](../ado-api/properties-collection-ado.md) ADO standard.  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](./axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di asse (VBScript)](./axis-example-vbscript.md)   
 [Raccolta assi (ADO MD)](./axes-collection-ado-md.md)   
 [Raccolta Positions (ADO MD)](./positions-collection-ado-md.md)   
 [Raccolta Properties (ADO)](../ado-api/properties-collection-ado.md)