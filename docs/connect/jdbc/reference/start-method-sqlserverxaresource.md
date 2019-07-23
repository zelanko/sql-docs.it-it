---
title: Metodo Start (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.start
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 33c90213-92f7-416b-b2fa-67a1afe64e97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cef1af2c416231892ea74a7def90237f84b036d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970037"
---
# <a name="start-method-sqlserverxaresource"></a>Metodo start (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Avvia il lavoro per conto di un ramo di transazione specificato nell'oggetto Xid.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void start(javax.transaction.xa.Xid xid,  
                  int flags)  
```  
  
#### <a name="parameters"></a>Parametri  
 *xid*  
  
 Oggetto XID.  
  
 *flags*  
  
 Valore **int** .  
  
## <a name="exceptions"></a>Eccezioni  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo start viene specificato dal metodo start nell'interfaccia javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
