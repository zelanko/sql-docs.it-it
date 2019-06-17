---
title: Metodo getMinutesOffset (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 18ba844a-ea36-42de-87da-bbc222082efe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6d17b5451340c07ea8c9bd0ce61bf858b419b121
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784761"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Metodo getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce l'offset, in pochi minuti rispetto all'ora GMT, di questo oggetto DateTimeOffset.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Offset in minuti.  
  
## <a name="remarks"></a>Remarks  
 Per un oggetto DateTimeOffset che rappresenta 8 marzo 2010, 11:35:48-0800, getMinutesOffset restituisce il valore 480.  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
