---
title: Metodo setime (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTime
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04ea83b2-db5e-4b46-b016-9e496363827e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81205764a663930ab2d555c0f231448c6cae4099
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972466"
---
# <a name="settime-method-sqlservercallablestatement"></a>Metodo setTime (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore di ora specificato.  
  
 A partire dal driver JDBC 3,0, il comportamento di questo metodo viene modificato dalla proprietà di connessione **sendTimeAsDatetime** ([impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|nome|Descrizione|  
|----------|-----------------|  
|[setTime (java.lang.String, java.sql.Time)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time.md)|Imposta il parametro designato sul valore di ora specificato.|  
|[setTime (java.lang.String, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time-java-util-calendar.md)|Imposta il parametro designato sui valori relativi all'ora e al calendario specificati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
