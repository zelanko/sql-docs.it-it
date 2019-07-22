---
title: Metodo getResultSetHoldability (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData,getResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f0bd6283-83ab-4a0a-b825-ec4cdccf03e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6fbf7a0cf66db8bbcc2f2f69d603bc5d32fb74d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980373"
---
# <a name="getresultsetholdability-method-sqlserverdatabasemetadata"></a>Metodo getResultSetHoldability (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la trattenibilità predefinita dei set di risultati del database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getResultSetHoldability()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica la trattenibilità predefinita.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getResultSetHoldability viene specificato dal metodo getResultSetHoldability nell'interfaccia java. SQL. DatabaseMetaData.  
  
 Quando si usa [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] questi metodi restituiscono 1, che equivale alla costante ResultSet.HOLD_CURSORS_OVER_COMMIT.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
