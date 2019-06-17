---
title: Last (metodo) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.last
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ac9bef59-8c31-437b-a183-619cc778fe7a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f97a3d27deeb4a51663cb108ab3adc77b75e29e8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790024"
---
# <a name="last-method-sqlserverresultset"></a>Metodo last (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore nell'ultima riga in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean last()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la nuova riga corrente è valida. **false** se sono presenti altre righe da elaborare.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo last viene specificato dal metodo last nell'interfaccia java.sql.ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
