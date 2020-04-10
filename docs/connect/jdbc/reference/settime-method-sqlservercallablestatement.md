---
title: Metodo setTime (SQLServerCallableStatement) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc546fd72aa53ec26c3b3385e7a5459464ae2dd4
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926579"
---
# <a name="settime-method-sqlservercallablestatement"></a>Metodo setTime (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il parametro designato sul valore di ora specificato.  
  
 A partire dal driver JDBC 3.0 di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il comportamento di questo metodo viene modificato dalla proprietà di connessione **sendTimeAsDatetime** ([Impostazione delle proprietà di connessione](../../../connect/jdbc/setting-the-connection-properties.md)) e [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Per altre informazioni, vedere [Configurazione della modalità di invio dei valori java.sql.Time al server](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Elenco degli overload  
  
|Nome|Descrizione|  
|----------|-----------------|  
|[setTime (java.lang.String, java.sql.Time)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time.md)|Imposta il parametro designato sul valore di ora specificato.|  
|[setTime (java.lang.String, java.sql.Time, java.util.Calendar)](../../../connect/jdbc/reference/settime-method-java-lang-string-java-sql-time-java-util-calendar.md)|Imposta il parametro designato sui valori relativi all'ora e al calendario specificati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
