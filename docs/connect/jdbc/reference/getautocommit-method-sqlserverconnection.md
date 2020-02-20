---
title: Metodo getAutoCommit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: af1f67f4-f568-4e58-abcc-5c809a89b547
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbd009f2052c911c469b842e2cd5353276d5d2c8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954049"
---
# <a name="getautocommit-method-sqlserverconnection"></a>Metodo getAutoCommit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la modalità di commit automatico corrente per questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean getAutoCommit()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se la modalità di commit automatico è abilitata. **false** in caso contrario.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo getAutoCommit viene specificato dal metodo getAutoCommit nell'interfaccia java.sql.Connection.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
