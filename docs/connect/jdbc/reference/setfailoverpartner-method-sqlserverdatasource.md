---
title: Metodo setFailoverPartner (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5310b7c2-9d10-474f-ad3a-218fe5da694b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d152001d1b0eb4ad47936d04ba6c74b8ae7f6e3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974276"
---
# <a name="setfailoverpartner-method-sqlserverdatasource"></a>Metodo setFailoverPartner (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il nome del server di failover utilizzato nella configurazione del mirroring del database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void setFailoverPartner(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parametri  
 *serverName*  
  
 Valore **String** contenente il nome del server di failover.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore impostato da questo metodo viene utilizzato nel caso di un errore di connessione iniziale al server principale. Dopo avere effettuato la connessione iniziale, questo valore viene ignorato. Insieme a questo metodo deve essere usato anche il metodo [setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md). In caso contrario, verrà generata un'eccezione.  
  
 Il driver non supporta la specifica del numero di porta del server di failover quando tale server viene impostato. È tuttavia supportata la chiamata al metodo [setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md) e al metodo [setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md) con il metodo [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
