---
title: Interfaccia ISQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f979ef1a15a07866e5331849130a7089acb1cea
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796425"
---
# <a name="isqlserverconnection-interface"></a>Interfaccia ISQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rappresenta una connessione JDBC a un database [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Questa interfaccia è stata aggiunta in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 **Pacchetto:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.sql.Connection  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>Remarks  
 Questa interfaccia viene implementata da [classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Questa interfaccia espone il campo specifico di [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] seguente:  
  
|Campo|Per ulteriori informazioni, vedere|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API del driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
