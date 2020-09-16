---
description: Metodo isAfterLast (SQLServerResultSet)
title: Metodo isAfterLast (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f0f982ebfce1e4920c98583f31bb7a9e14ba867
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433673"
---
# <a name="isafterlast-method-sqlserverresultset"></a>Metodo isAfterLast (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera informazioni sull'eventuale presenza del cursore nella posizione successiva all'ultima riga in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se il cursore si trova dopo l'ultima riga. **false** se il cursore si trova in un'altra posizione o se il set di risultati non contiene righe.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo isAfterLast viene specificato dal metodo isAfterLast nell'interfaccia java.sql.ResultSet.  
  
 Se questo metodo viene utilizzato con cursori dinamici, inclusi i cursori di sola lettura forward-only, e la proprietà di connessione selectMethod viene impostata su "cursor", si verificherà un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
