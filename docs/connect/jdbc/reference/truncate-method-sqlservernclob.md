---
title: Metodo truncate (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7e8210d-a724-4bae-832a-ae4c63031c9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9ed19679cb1a173d015152a006f55660fe9f826
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67968468"
---
# <a name="truncate-method-sqlservernclob"></a>Metodo truncate (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Tronca l'oggetto **NCLOB** in base alla lunghezza specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void truncate(long len)  
```  
  
#### <a name="parameters"></a>Parametri  
 *len*  
  
 Lunghezza espressa in caratteri, in base alla quale deve essere troncato l'oggetto **NCLOB**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo truncate viene specificato dal metodo truncate nell'interfaccia java.sql.NClob.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membri di SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
