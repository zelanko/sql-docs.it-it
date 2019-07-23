---
title: Metodo commit (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.commit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c7346165-51bf-4844-b64c-29833c147236
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7561a77d91ca7de4aafd9a5d7aab2c9a4b312124
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955560"
---
# <a name="commit-method-sqlserverconnection"></a>Metodo commit (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Rende permanenti tutte le modifiche apportate dal commit o dal rollback precedente e rilascia eventuali blocchi del database contenuti in questo oggetto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void commit()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo commit viene specificato dal metodo commit nell'interfaccia java.sql.Connection.  
  
 Questo metodo deve essere utilizzato solo quando la modalità autocommit è stata disabilitata.  
  
 Si noti che questo metodo avrà esito negativo e genererà un'eccezione se il client avvia una transazione manuale e se successivamente, per qualche motivo, SQL Server esegue il rollback della transazione manuale. Ad esempio, viene generata un'eccezione se il client chiama una stored procedure che chiama in modo esplicito ROLLBACK TRANSACTION e se il client chiama quindi il metodo commit. Inoltre, se SQL Server genera un errore la cui gravità è sufficiente (almeno 16) per eseguire il rollback della transazione manuale avviata dal client, una chiamata successiva al metodo commit genererà un'eccezione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
