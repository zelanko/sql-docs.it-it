---
title: Metodo Close (ADO MD) | Microsoft Docs
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
ms.openlocfilehash: 09e83fd8645a5c0ab604a640478c4cced4870742
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949819"
---
# <a name="close-method-ado-md"></a>Metodo Close (ADO MD)
Chiude un celle aperto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Osservazioni  
 Se si utilizza il metodo **Close** per chiudere un oggetto di un [celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) , i dati associati vengono rilasciati, inclusi i dati in tutti gli oggetti [Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [position](../../../ado/reference/ado-md-api/position-object-ado-md.md)o [member](../../../ado/reference/ado-md-api/member-object-ado-md.md) correlati. La chiusura di un **celle** non viene rimossa dalla memoria; è possibile modificare le impostazioni delle proprietà e riaprirle in un secondo momento. Per eliminare completamente un oggetto dalla memoria, impostare la variabile oggetto su **Nothing**.  
  
 In un secondo momento è possibile chiamare il metodo [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) per riaprire il **cellt** usando la stessa stringa di origine o un'altra. Mentre l'oggetto di **celle** è chiuso, il recupero di qualsiasi proprietà o la chiamata di metodi che fanno riferimento ai dati o ai metadati sottostanti genera un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Oggetto member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Metodo Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Oggetto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [Proprietà State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
