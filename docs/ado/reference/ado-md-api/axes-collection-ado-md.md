---
title: Raccolta assi (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c06faf6327d60be823ce9d99215655b5badf5e3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947402"
---
# <a name="axes-collection-ado-md"></a>Raccolta Axes (ADO MD)
Contiene gli oggetti [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md) che definiscono un oggetto Cell.  
  
## <a name="remarks"></a>Osservazioni  
 Un oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) contiene una raccolta di **assi** . Una volta aperto il gruppo di **celle** , questa raccolta conterrà almeno un **asse**. Per una spiegazione più dettagliata dell'utilizzo degli oggetti **asse** , vedere l'oggetto [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md) .  
  
> [!NOTE]
>  L'asse del filtro di un gruppo di **celle** non è contenuto nella raccolta **assi** . Per ulteriori informazioni, vedere la proprietà [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) .  
  
 **Assi** è una raccolta ADO standard. Con le proprietà e i metodi di una raccolta, è possibile eseguire le operazioni seguenti:  
  
-   Ottenere il numero di oggetti nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Restituisce un oggetto dalla raccolta con la proprietà dell' [elemento](../../../ado/reference/ado-api/item-property-ado.md) predefinito.  
  
-   Aggiornare gli oggetti della raccolta dal provider con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di celle (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Oggetto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
