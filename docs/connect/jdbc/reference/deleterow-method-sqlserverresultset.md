---
title: Metodo deleteRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987be5ee9fd49385acf02e52108e1e657fbc08a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786520"
---
# <a name="deleterow-method-sqlserverresultset"></a>Metodo deleteRow (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Elimina la riga corrente da questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) e dal database sottostante.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo deleteRow viene specificato dal metodo deleteRow nell'interfaccia ResultSet.  
  
 Non è possibile chiamare questo metodo quando il cursore si trova sulla riga di inserimento.  
  
 In caso di uso di cursori keyset, questo metodo lascia uno spazio nel set di risultati. È possibile verificare la presenza di questo spazio tramite il metodo [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). I numeri delle righe del set di risultati non cambiano.  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
