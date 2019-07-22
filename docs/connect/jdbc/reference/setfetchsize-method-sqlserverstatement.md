---
title: Metodo setFetchSize (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58af3c6d8b9d0967ff370047e49a377bf52ec985
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974234"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>Metodo setFetchSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornisce a [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] un hint per il numero di righe che devono essere recuperate dal database, quando sono necessarie più righe.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parametri  
 *rows*  
  
 Valore **int** che indica il numero di righe da recuperare.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setFetchSize viene specificato dal metodo setFetchSize nell'interfaccia java. SQL. Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
