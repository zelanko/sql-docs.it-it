---
title: Metodo getGeneratedKeys (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getGeneratedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3325950-0e81-4ae8-aa0c-e1f6d371adcd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d47ff96fe493053e7a953cfbae53e52be95a0d62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982946"
---
# <a name="getgeneratedkeys-method-sqlserverstatement"></a>Metodo getGeneratedKeys (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera le chiavi generate automaticamente create come risultato dell'esecuzione di questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final java.sql.ResultSet getGeneratedKeys()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto ResultSet.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getGeneratedKeys viene specificato dal metodo getGeneratedKeys nell'interfaccia java. SQL. Statement.  
  
 Per ulteriori informazioni sull'utilizzo di questo metodo, vedere [utilizzo delle chiavi generate automaticamente](../../../connect/jdbc/using-auto-generated-keys.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
