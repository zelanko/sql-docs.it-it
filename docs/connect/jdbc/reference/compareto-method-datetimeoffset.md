---
title: Metodo compareTo (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f70413a7624b9bbd380a664fbf61b9a33f8989b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955511"
---
# <a name="compareto-method-datetimeoffset"></a>Metodo compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Confronta questo oggetto **DateTimeOffset** con un altro oggetto **DateTimeOffset** in base all'ora GMT.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parametri  
 Valore [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) che si vuole confrontare con l'istanza corrente.  
  
## <a name="return-value"></a>Valore restituito  
 Nella tabella seguente viene descritto il valore restituito del metodo:  
  
|Valore restituito|Descrizione|  
|------------------|-----------------|  
|0|Entrambi gli oggetti **DateTimeOffset** rappresentano lo stesso punto nel tempo.|  
|numero negativo|Questo oggetto **DateTimeOffset** rappresenta un punto nel tempo precedente all' *altro*.|  
|numero positivo|Questo oggetto **DateTimeOffset** rappresenta un punto nel tempo successivo a un *altro*.|  
  
## <a name="remarks"></a>Remarks  
 Quando due oggetti **DateTimeOffset** specificano la stessa ora GMT, non viene applicato alcun ordinamento aggiuntivo in base alla differenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
