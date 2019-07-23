---
title: Metodo setime (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setTime
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3a83ea3-6636-4096-842b-71b37340fa07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4b11b2d25abec8717604948101ca81d651fe822
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972455"
---
# <a name="settime-method-sqlserverpreparedstatement"></a>Metodo setTime (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore di ora specificato.  
  
 A partire dal driver JDBC 3,0, il comportamento di questo metodo viene modificato dalla proprietà di connessione **sendTimeAsDatetime** ([impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per ulteriori informazioni, vedere [configurazione della modalità di invio dei valori java. SQL. Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|nome|Descrizione|  
|----------|-----------------|  
|[setTime (int, java.sql.Time)](../../../connect/jdbc/reference/settime-method-int-java-sql-time.md)|Imposta il parametro designato sul valore di ora specificato.|  
|[setTime (int, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-int-java-sql-time-java-util-calendar.md)|Imposta il parametro designato sui valori relativi all'ora e al calendario specificati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
