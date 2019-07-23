---
title: Metodo setInt (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setInt
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7de05cf4-3a48-4c60-9a1b-6ad2ae43d258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45361c22d1e453b12f8bedf2fba2a4c10f02de0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974192"
---
# <a name="setint-method-sqlservercallablestatement"></a>Metodo setInt (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore **int** specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setInt(java.lang.String sCol,  
                   int i)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *i*  
  
 Valore **int** .  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setInt viene specificato dal metodo setInt nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
