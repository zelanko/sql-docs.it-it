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
manager: jroth
ms.openlocfilehash: cb06138639be09378baa8dfe94d110c0ded41223
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777367"
---
# <a name="compareto-method-datetimeoffset"></a>Metodo compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Confronta questo **DateTimeOffset** oggetto a altra **DateTimeOffset** oggetto in base all'ora gtm.  
  
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
|0|Entrambe **DateTimeOffset** oggetti rappresentano lo stesso punto nel tempo.|  
|numero negativo|Ciò **DateTimeOffset** oggetto rappresenta un punto nel tempo che precede *altri*.|  
|numero positivo|Ciò **DateTimeOffset** oggetto rappresenta un punto nel tempo successivo *altri*.|  
  
## <a name="remarks"></a>Remarks  
 Quando due oggetti **DateTimeOffset** specificano la stessa ora GMT, non viene applicato alcun ordinamento aggiuntivo in base alla differenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membri di DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
