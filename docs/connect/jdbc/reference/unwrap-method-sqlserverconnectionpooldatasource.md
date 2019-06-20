---
title: Metodo Unwrap (SQLServerConnectionPoolDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f5c9b734-2096-4ae4-a284-6b4d1b4a00d4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 51c3a41c0c46345efc83247e6fe45140c6054b62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66799588"
---
# <a name="unwrap-method-sqlserverconnectionpooldatasource"></a>Metodo unwrap (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce un oggetto che implementa l'interfaccia specificata per consentire l'accesso ai metodi specifici di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parametri  
 *iface*  
  
 Classe di tipo **T** che definisce un'interfaccia.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto che implementa l'interfaccia specificata.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Il metodo [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md) è definito dall'interfaccia java.sql.Wrapper, introdotta nella specifica JDBC 4.0.  
  
 È possibile che le applicazioni debbano accedere alle estensioni dell'API JDBC specifiche di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Il metodo unwrap supporta l'annullamento del wrapping nelle classi pubbliche estese dall'oggetto, se le classi espongono estensioni del fornitore.  
  
 La classe [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) estende la classe [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md). Quando viene chiamato questo metodo, l'oggetto annulla il wrapping nelle classi [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) e [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md).  
  
 Per altre informazioni, vedere [wrapper e interfacce](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [Membri di SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Classe SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
