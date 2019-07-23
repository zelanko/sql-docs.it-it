---
title: Metodo Forget (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.forget
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d83138d-aa45-4d94-9da6-fdfe7ed28edc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5eaaa98b2d79dc29558d32a254d338c9891372f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954540"
---
# <a name="forget-method-sqlserverxaresource"></a>Metodo forget (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica allo strumento di gestione delle risorse di dimenticare un ramo di transazione completato euristicamente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void forget(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>Parametri  
 *xid*  
  
 Oggetto XID.  
  
## <a name="exceptions"></a>Eccezioni  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo forget viene specificato dal metodo forget nell'interfaccia javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membri di SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
