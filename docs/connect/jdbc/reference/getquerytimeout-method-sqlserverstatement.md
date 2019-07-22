---
title: Metodo getQueryTimeout (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8dff954f-b458-4fa6-abe6-be62ff75e2b9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fd4d7b32c9480fec28e20a9dcbc9c22530eb4a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980647"
---
# <a name="getquerytimeout-method-sqlserverstatement"></a>Metodo getQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il numero di secondi di attesa di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] prima dell'esecuzione di questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final int getQueryTimeout()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il numero di secondi di attesa del driver JDBC oppure 0 se non esiste alcun limite.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getQueryTimeout viene specificato dal metodo getQueryTimeout nell'interfaccia java. SQL. Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
