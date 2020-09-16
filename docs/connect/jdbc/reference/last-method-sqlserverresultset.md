---
description: Metodo last (SQLServerResultSet)
title: Metodo last (SQLServerResultSet) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21c7e2c503d3f62548fd9804e2af2cdba6eae852
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433263"
---
# <a name="last-method-sqlserverresultset"></a>Metodo last (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sposta il cursore nell'ultima riga in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean last()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la nuova riga corrente è valida. **false** se non sono presenti altre righe da elaborare.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo last viene specificato dal metodo last nell'interfaccia java.sql.ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
