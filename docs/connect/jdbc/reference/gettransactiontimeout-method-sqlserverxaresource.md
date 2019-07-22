---
title: Metodo getTransactionTimeout (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.getTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed0a37e9-1132-4d3f-b88f-8be674e852b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7aa67a0d4cc8a218500d278783f9dc8b6026fb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978620"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>Metodo getTransactionTimeout (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ottiene il valore del timeout della transazione corrente impostato per questo oggetto [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getTransactionTimeout viene specificato dal metodo getTransactionTimeout nell'interfaccia javax. Transaction. XA. XAResource.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
