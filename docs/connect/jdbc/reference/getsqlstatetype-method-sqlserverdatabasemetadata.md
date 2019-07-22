---
title: Metodo getSQLStateType (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76faa3bcaccac4f75d95dc49276c669a5631b5a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979729"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>Metodo getSQLStateType (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se il valore SQLSTATE restituito dal metodo SQLException.getSQLState è X/Open (ora noto come Open Group), SQL CLI, SQL99 (JDBC 3.0) o SQL:2003 (JDBC 4.0).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **int** che indica il tipo di SQLSTATE. Può essere uno dei valori seguenti:  
  
-   Per Java Runtime Environment versione 5,0: se la proprietà di connessione **xopenStates** è impostata su **true**, questo metodo restituisce DatabaseMetaData. sqlStateXOpen. In caso contrario, DatabaseMetaData. sqlStateSQL99.  
  
-   Per Java Runtime Environment versione 6,0: se la proprietà di connessione **xopenStates** è impostata su **true**, questo metodo restituisce DatabaseMetaData. sqlStateXOpen. In caso contrario, DatabaseMetaData. sqlStateSQL.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getSQLStateType viene specificato dal Metodo getSQLStateType nell'interfaccia java. SQL. DatabaseMetaData.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membri di SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
