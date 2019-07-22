---
title: Metodo Cancel (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04f3461743801e69248362710197ce2d4c31384f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955787"
---
# <a name="cancel-method-sqlserverstatement"></a>Metodo cancel (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Annulla l'istruzione SQL attualmente in esecuzione tramite questo oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo cancel viene specificato dal metodo cancel nell'interfaccia java.sql.Statement.  
  
 Quando si esegue un'istruzione che genera un solo set di risultati forward-only di sola lettura di grandi dimensioni, si potrebbe essere interessati solo a qualche set di righe iniziale nel set di risultati restituito. In questo caso, l'applicazione potrebbe chiamare il metodo [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) dell'oggetto istruzione associato prima di chiudere il set di risultati in modo da ridurre al minimo il tempo di elaborazione necessario per rimuovere le righe rimanenti non necessarie. Al momento di decidere se utilizzare o meno questa tecnica, si consiglia di tenere conto della necessità di mantenere un equilibrio tra il tempo di elaborazione salvato e il tempo e il round trip al server aggiuntivo necessari per annullare l'esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
