---
title: Metodo executeBatch (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8418167e-cbd2-464d-b118-73cdd76080ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 463106c14a63feddb68998affff8131933e81dfa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954893"
---
# <a name="executebatch-method-sqlserverpreparedstatement"></a>Metodo executeBatch (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Invia al database un batch di comandi da eseguire. Se tutti i comandi vengono eseguiti correttamente, restituisce una matrice di conteggi aggiornamenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Matrice di valori interi contenente i conteggi aggiornamenti.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo executeBatch viene specificato dal metodo executeBatch nell'interfaccia java.sql.Statement.  
    
 Questo metodo esegue l'override di [SQLServerStatement.executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
