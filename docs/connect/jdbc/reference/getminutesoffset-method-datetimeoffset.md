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
ms.openlocfilehash: 6af552920698d4eb149f5edd5ee50128db0e1b61
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67981805"
---
# <a name="getminutesoffset-method-datetimeoffset"></a>Metodo getMinutesOffset (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce l'offset, in minuti dall'ora GMT, di questo oggetto DateTimeOffset.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getMinutesOffset()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Offset in minuti.  
  
## <a name="remarks"></a>Osservazioni  
 Per un oggetto DateTimeOffset che rappresenta l'8 marzo 2010, 11:35:48 -0800, getMinutesOffset restituisce il valore 480.  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
