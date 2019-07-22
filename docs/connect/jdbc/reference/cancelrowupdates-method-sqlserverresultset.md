---
title: Metodo cancelRowUpdates (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1598bca994ae41ccee56ca68e12e74e8d18fd0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955794"
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>Metodo cancelRowUpdates (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Annulla gli aggiornamenti eseguiti alla riga corrente in questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo cancelRowUpdates viene specificato dal metodo cancelRowUpdates nell'interfaccia java. SQL. ResultSet.  
  
 Questo metodo può essere chiamato dopo la chiamata di un metodo di aggiornamento e prima della chiamata del metodo [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) per eseguire il rollback degli aggiornamenti apportati a una riga. Se non è stato apportato alcun aggiornamento o il metodo updateRow è già stato chiamato, questo metodo non ha effetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
