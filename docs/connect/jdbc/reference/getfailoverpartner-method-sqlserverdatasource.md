---
description: Metodo getFailoverPartner (SQLServerDataSource)
title: Metodo getFailoverPartner (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607f14bab8795ba3dfebd33e2c179f85897f210a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436063"
---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>Metodo getFailoverPartner (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Restituisce il nome del server di failover utilizzato nella configurazione del mirroring del database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String** contenente il nome del partner di failover oppure Null se non ne è impostato alcuno.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore restituito da questo metodo riflette il nome del partner di failover impostato usando il metodo [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
