---
title: Metodo supportsMinimumSQLGrammar (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMinimumSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 40f5d727-1ce7-414d-867d-589ead7b2a29
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 970f2989b771fc319b77081693bd1dd7809b203d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969295"
---
# <a name="supportsminimumsqlgrammar-method-sqlserverdatabasemetadata"></a>Metodo supportsMinimumSQLGrammar (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera un valore che indica se il database supporta la grammatica SQL minima ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public boolean supportsMinimumSQLGrammar()  
```  
  
## <a name="return-value"></a>Valore restituito  
 **true** se supportato. In caso contrario, **false**.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo supportsMinimumSQLGrammer viene specificato dal metodo supportsMinimumSQLGrammer nell'interfaccia java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
