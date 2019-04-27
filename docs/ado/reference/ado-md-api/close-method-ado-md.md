---
title: Close (metodo) (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca61f383198207223abf30ce25d9c922909f6526
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653501"
---
# <a name="close-method-ado-md"></a>Metodo Close (ADO MD)
Chiude un set di celle open.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Note  
 Usando il **chiudere** metodo per chiudere un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto rilascerà i dati associati, inclusi i dati in qualsiasi correlati [celle](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md), o [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetti. Chiusura di un **Cellset** senza rimuoverlo dalla memoria; è possibile modificare le impostazioni delle proprietà e aprirlo più tardi. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto **Nothing**.  
  
 In un secondo momento, è possibile chiamare il [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) metodo per riaprire il **set di celle** usando lo stesso o in un'altra stringa di origine. Mentre il **Cellset** oggetto è chiuso, il recupero di qualsiasi proprietà o chiamare i metodi che fanno riferimento i dati sottostanti o dei metadati viene generato un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Metodo Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Oggetto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [Proprietà State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
