---
description: Raccolta Axes (ADO MD)
title: Raccolta assi (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 78113cb7854ec3f56ffe6f7322a6bb732939f27f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987412"
---
# <a name="axes-collection-ado-md"></a>Raccolta Axes (ADO MD)
Contiene gli oggetti [asse](./axis-object-ado-md.md) che definiscono un oggetto Cell.  
  
## <a name="remarks"></a>Osservazioni  
 Un oggetto [cellt](./cellset-object-ado-md.md) contiene una raccolta di **assi** . Una volta aperto il gruppo di **celle** , questa raccolta conterrà almeno un **asse**. Per una spiegazione più dettagliata dell'utilizzo degli oggetti **asse** , vedere l'oggetto [asse](./axis-object-ado-md.md) .  
  
> [!NOTE]
>  L'asse del filtro di un gruppo di **celle** non è contenuto nella raccolta **assi** . Per ulteriori informazioni, vedere la proprietà [FilterAxis](./filteraxis-property-ado-md.md) .  
  
 **Assi** è una raccolta ADO standard. Con le proprietà e i metodi di una raccolta, è possibile eseguire le operazioni seguenti:  
  
-   Ottenere il numero di oggetti nella raccolta con la proprietà [count](../ado-api/count-property-ado.md) .  
  
-   Restituisce un oggetto dalla raccolta con la proprietà dell' [elemento](../ado-api/item-property-ado.md) predefinito.  
  
-   Aggiornare gli oggetti della raccolta dal provider con il metodo [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](./axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di celle (VB)](./cellset-example-vb.md)   
 [Oggetto Axis (ADO MD)](./axis-object-ado-md.md)