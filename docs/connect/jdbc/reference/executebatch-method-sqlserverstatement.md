---
title: Metodo executeBatch (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeBatch
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fb034f63-2532-4da8-a1b0-bc125734585a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9a4a93ccd16fccd90db0a5bb5e4e234ea3a939a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802300"
---
# <a name="executebatch-method-sqlserverstatement"></a>Metodo executeBatch (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Invia al database un batch di comandi da eseguire. Se tutti i comandi vengono eseguiti correttamente, restituisce una matrice di conteggi aggiornamenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public int[] executeBatch()  
```  
  
## <a name="return-value"></a>Valore restituito  
 Matrice di valori **int** contenente i conteggi aggiornamenti.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
 java.sql.BatchUpdateException  
  
## <a name="remarks"></a>Remarks  
 Questo metodo executeBatch viene specificato dal metodo executeBatch nell'interfaccia Statement.  
  
 Dopo aver inviato i comandi al database, questo metodo cancella qualsiasi comando del batch.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
