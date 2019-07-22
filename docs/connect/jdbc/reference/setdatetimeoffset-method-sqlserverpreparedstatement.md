---
title: Metodo sedatetimeoffset (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5014dba9-1755-4769-b070-6cbeecee864e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 429e1720a6fac8c01ce2d201717787146bc8cc63
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974359"
---
# <a name="setdatetimeoffset-method-sqlserverpreparedstatement"></a>Metodo setDateTimeOffset (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Questo metodo è stato aggiunto in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] JDBC Driver 3.0 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Imposta il valore della colonna specificata sul valore della [classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setDateTimeOffset(int n, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>Parametri  
 *n*  
  
 Numero ordinale in base zero di una colonna.  
  
 *x*  
  
 Oggetto della [classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) .  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
