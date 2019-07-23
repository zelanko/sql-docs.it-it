---
title: Metodo getBigDecimal (int, int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c99d0772-b26c-492c-a643-2813b5429993
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15991cb98860ccc471229ae3abb8e3b24e35c799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954018"
---
# <a name="getbigdecimal-method-int-int-sqlserverresultset"></a>Metodo getBigDecimal (int, int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera il valore dell'indice di colonna designato nella riga corrente di questo oggetto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) tramite la scala specificata.  
  
> [!NOTE]  
>  Questo metodo è stato dichiarato deprecato dalla specifica JDBC. È invece necessario usare il metodo [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int-sqlserverresultset.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
public java.math.BigDecimal getBigDecimal(int columnIndex,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parametri  
 *columnIndex*  
  
 Valore **int** che indica l'indice di colonna.  
  
 *scala*  
  
 Valore **int** che indica il numero di cifre a destra del separatore decimale.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto BigDecimal.  
  
## <a name="exceptions"></a>Eccezioni  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Questo metodo getBigDecimal viene specificato dal Metodo getBigDecimal nell'interfaccia java. SQL. ResultSet.  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo getBigDecimal &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [Membri di SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
