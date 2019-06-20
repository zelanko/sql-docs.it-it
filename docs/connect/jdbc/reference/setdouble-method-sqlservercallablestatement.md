---
title: Metodo setDouble (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setDouble
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c054bb84-1292-4b70-b574-2ae189cd4e68
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4ac0606af5e58c237580c240689f7940af74f83c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801614"
---
# <a name="setdouble-method-sqlservercallablestatement"></a>Metodo setDouble (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore **double** specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setDouble(java.lang.String sCol,  
                      double d)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Valore **String** contenente il nome del parametro.  
  
 *d*  
  
 Oggetto **doppie** valore.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setDouble viene specificato dal metodo setDouble nell'interfaccia java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
