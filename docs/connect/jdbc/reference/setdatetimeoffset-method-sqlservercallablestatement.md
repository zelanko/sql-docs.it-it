---
title: Metodo sedatetimeoffset (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9383e14d-c83e-43c5-980c-50a3e0bedc31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 264de7ac150aca7494a380fbbd4f5b490607c5c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974639"
---
# <a name="setdatetimeoffset-method-sqlservercallablestatement"></a>Metodo setDateTimeOffset (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Questo metodo è stato aggiunto in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] JDBC Driver 3.0 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Imposta il valore della colonna specificata sul valore della [classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setDateTimeOffset(String sCol, microsoft.sql.DateTimeOffset t)  
```  
  
#### <a name="parameters"></a>Parametri  
 *sCol*  
  
 Nome di una colonna.  
  
 *t*  
  
 Oggetto della [classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) .  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 È possibile recuperare un valore di [classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) con [SQLServerCallableStatement. GetDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md).  
  
 il numero ordinale della colonna viene preso da [DateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
