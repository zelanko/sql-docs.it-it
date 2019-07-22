---
title: Metodo setQueryTimeout (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a4a271e07dea5a533dcb19b098a3e3de29e535e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973177"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>Metodo setQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Imposta il numero di secondi durante i quali il driver rimarrà in attesa dell'esecuzione di un oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) sul numero di secondi specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parametri  
 *secondi*  
  
 Valore **int** che indica il numero di secondi di attesa oppure 0 se non esiste alcun limite.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo setQueryTimeout viene specificato dal metodo setQueryTimeout nell'interfaccia java. SQL. Statement.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
